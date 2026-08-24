---
title: Block Internet on a Schedule
excerpt: >-
  Use flexible weekly Endpoint Schedules to block Internet access at specific
  times.
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

Endpoint Schedules apply a selected [Profile](doc:profiles) during one or more weekly time windows. Outside those windows, the Endpoint uses its normal **Enforced Profile**.

A single Schedule can contain:

- Different time windows for each day of the week
- Multiple windows and Profiles on the same day
- Minute-precise start and end times
- A specific timezone, so the Schedule follows local time

This makes it useful for parental controls, office hours, study time, maintenance windows, or any other recurring policy change.

## Create a Profile that blocks Internet access

1. Create a new [Profile](doc:profiles) with a clear name, such as **Block Everything**.
2. Open the Profile and create a [Default Rule](doc:default-rule) that blocks all traffic.

You will assign this Profile to the time windows when Internet access should be disabled.

## Create a weekly Schedule

1. Go to [Endpoints](https://controld.com/dashboard/endpoints).
2. Edit the Endpoint you want to schedule. If it is a new Endpoint, save it before creating the Schedule.
3. Select the Schedule icon beside **Enforced Profile**.
4. Confirm the **Timezone** shown below the calendar. Schedule times are evaluated in this timezone.
5. Add a time window:
   - On desktop or tablet, drag across a day in the calendar.
   - On mobile, tap the start time and then the end time.
6. Choose the Profile to enforce during that window. To block Internet access, select **Block Everything**.
7. Add any other windows you need. You can assign different Profiles to different windows.
8. Use the copy icon beside a day to copy all of that day's windows to one or more other days.
9. Select **Save schedule**.

> 📘 Time window rules
>
> The calendar uses 30-minute slots when dragging, but you can type exact minutes into the **Start** and **End** fields. Each window must be at least 30 minutes long, and windows on the same day cannot overlap.

The selected Profile is applied automatically when a window starts. When it ends, the Endpoint returns to its normal Enforced Profile unless another Schedule window begins.

## Overnight Schedules

An overnight period crosses midnight, so create two windows:

- One from the desired start time to the end of the first day
- One from midnight to the desired end time on the following day

For example, to block Internet access from **5:00 PM Monday until 9:00 AM Tuesday**:

1. Add a Monday window from **17:00 to the end of the day** using **Block Everything**.
2. Add a Tuesday window from **00:00 to 09:00** using **Block Everything**.

Repeat or copy the windows for the other days you want covered. You no longer need to reverse the normal and blocking Profiles as a workaround for overnight schedules.

## Common setups

| Goal | Endpoint's normal Enforced Profile | Scheduled windows |
| --- | --- | --- |
| Block Internet during selected hours | Your normal Profile | Apply **Block Everything** during blocked hours |
| Allow Internet only during selected hours | **Block Everything** | Apply your normal Profile during allowed hours |
| Use different policies throughout the day | Your usual default Profile | Assign the appropriate Profile to each window |

## Edit or remove a Schedule

Edit the Endpoint and select the Schedule icon again.

- Select a window to change its time or assigned Profile.
- Use **Remove window** to delete one window.
- Use **Clear all**, then **Save schedule**, to remove the Schedule entirely.
- Change the Schedule's timezone from the timezone selector below the calendar.

The Endpoint shows **Weekly Schedule** and the number of configured windows when a Schedule is present.
