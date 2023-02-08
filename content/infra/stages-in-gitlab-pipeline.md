---
title: 'Stages in Gitlab Pipeline'
date: 2023-02-08T09:58:26+05:30
draft: true
---

# `allow_failure`

If value to this stage is set to

- `true` : even if that job fails then rest of the pipeline will continue.
- `false` : then pipeline will fail & will be marked as failed.

# `when`

This field is used to configure when that particular job must run. We can give following values to this field

- `on_success` : run when all jobs in prior stage have succed.
- `manual` : run when someone manually triggers it.
- `always` : run regardless of status of previous stage.
- `on_failure` : run when at least one job have failed in prior stage.
- `delayed` : delay the execution of job for specific period of time.
- `never` : never run the job.
