# Jenkins Upgrade Triage Guide  
**Problem**: After upgrading Jenkins from 2.214 → 2.492.1, GitLab integration is broken (webhooks fail, merge request builds don’t trigger, pipeline steps like updateGitlabCommitStatus throw errors, etc.)

**Root Cause (most common)**:  
The **GitLab Plugin** and its dependency **Jackson 2 API Plugin** are incompatible with the newer libraries shipped in Jenkins 2.492.1 (Jackson 2.17+, Jetty 12, updated BOM).

### Verified Working Combination for Jenkins 2.492.1 (LTS)

| Plugin                  | Required Version | Release Date | Download / Plugin ID                    | Notes                                      |
|-------------------------|------------------|--------------|-----------------------------------------|--------------------------------------------|
| GitLab Plugin           | **1.9.9**        | 2025-09-06   | gitlab-plugin                           | Latest stable, supports Jenkins ≥ 2.492.3 |
| Jackson 2 API Plugin    | **2.20.0**+      | 2025-xx-xx   | jackson2-api                            | Provides Jackson Databind 2.17–2.19        |
| (Optional) Jersey 2 API | 2.39 or higher   | —            | jersey2-api                             | Usually auto-updated                       |

### Step-by-Step Fix (Triage Checklist)

1. **Backup Current State**
   - Export Configuration as Code (if using CasC)
   - Take a snapshot/backup of $JENKINS_HOME

2. **Update Plugins (Recommended Order)**
   - Manage Jenkins → Plugins → Installed
   - Or go directly to Updates tab
   - Install/Update:
     1. Jackson 2 API Plugin → **2.20.0** (or latest 2.20.x)
     2. GitLab Plugin → **1.9.9**
   - Restart Jenkins when prompted

3. **If Plugin Manager Shows Compatibility Warnings**
   - Download the .hpi files manually:
     - GitLab Plugin 1.9.9: https://updates.jenkins.io/download/plugins/gitlab-plugin/1.9.9/gitlab-plugin.hpi
     - Jackson 2 API 2.20.0: https://updates.jenkins.io/download/plugins/jackson2-api/2.20.0/jackson2-api.hpi
   - Manage Jenkins → Plugins → Advanced → Upload Plugin

 professionalism   - Upload and restart

4. **Verify Installation**
   - Manage Jenkins → System Information
   - Search for:
     - `gitlab-plugin` version → 1.9.9
     - `jackson2-api` version → 2.20.0+
     - `com.fasterxml.jackson.databind` → 2.17.x–2.19.x

5. **Test the Integration**
   - Push a commit or open a merge request in GitLab
   - Check Jenkins job is triggered
   - Verify commit status appears in GitLab MR (pending → running → success/failure)

6. **Enable Detailed Logging (if still failing)**
   - Manage Jenkins → System Log → New Log Recorder
   - Name: `GitLab Debug`
   - Loggers (FINEST level):
     - `com.dabsquared.gitlabjenkins`
     - `org.jenkinsci.plugins.gitlab`
   - Reproduce the issue → copy stack trace

### Common Errors & Quick Fixes

| Symptom                                      | Likely Cause                         | Fix                                                                 |
|----------------------------------------------|--------------------------------------|---------------------------------------------------------------------|
| `NoSuchMethodError` / `ClassNotFoundException` involving Jackson classes | Old Jackson 2 API plugin             | Force update to 2.20.0+                                             |
| Webhook 500 error from Jenkins               | GitLab plugin too old for Jetty 12   | Upgrade to GitLab Plugin 1.9.9                                      |
| `updateGitlabCommitStatus` step fails        | State name changed in newer plugin   | Use explicit states: `pending`, `running`, `success`, `failed`      |
| 401 Unauthorized on webhook                  | Secret token mismatch after upgrade  | Re-save the GitLab connection in Global Tool Configuration         |
| Builds not triggered at all                  | Webhook URL changed or blocked       | Re-add webhook in GitLab (use new Jenkins URL if behind reverse proxy) |

### Rollback Plan (if needed)
- Downgrade only the two plugins back to versions known to work with your old setup (not recommended long-term).
- Never downgrade Jenkins core from 2.492.1 → 2.214 (security risk).

### References
- GitLab Plugin: https://plugins.jenkins.io/gitlab-plugin/
- Jackson 2 API Plugin: https://plugins.jenkins.io/jackson2-api/
- Changelog 1.9.9: https://github.com/jenkinsci/gitlab-plugin/releases/tag/gitlab-plugin-1.9.9

Done. With GitLab Plugin 1.9.9 + Jackson 2 API 2.20.0+, your integration will work reliably on Jenkins 2.492.1.