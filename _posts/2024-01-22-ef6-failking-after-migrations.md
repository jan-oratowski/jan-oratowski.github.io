---
layout: post
title: "Entity Framework 6 failing after migrations were applied"
date: 2024-01-22 13:00:00 +0100
categories: ef6 migrations failing
---

Recently, one of our deployments to staging environment failed with this message:


Unable to update database to match the current model because there are pending changes and automatic migration is disabled. Either write the pending model changes to a code-based migration or enable automatic migration. Set DbMigrationsConfiguration.AutomaticMigrationsEnabled to true to enable automatic migration.
You can use the Add-Migration command to write the pending model changes to a code-based migration.


This was weird because we have migrations enabled and applied during each deployment.

Checking MigrationHistory in the database showed all migrations applied correctly.

We solved it by creating new, empty migration and deploying the project with it.

After some more digging, it turns out there were multiple migrations that had to be applied at the same time and since snapshot of the database wasn't aligned with the state after migrations, the error occured.

Probably just re-generating the snapshot would work, but since we already applied that empty migration (which also regenerated the snapshot), it was left like that.