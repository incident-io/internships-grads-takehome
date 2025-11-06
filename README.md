# Internships, placements and graduates

[job-ad]: https://incident.io/careers#open-roles

We're on a mission to build the single place you turn to when things go wrong. Over the past year, we’ve also built some of the most ambitious AI-native features in our space. From ways to make incident response smoother, to AI agents that investigate, explain, and even fix issues, we’re reimagining what incident management can be.

incident.io is now offering internships, placements, and graduate programmes for student engineers, 
providing you the chance to be at the forefront of innovation through 3-month, 6-month, 1-year placements, or by joining as a full-time graduate.

## What is the role?

This application is for a Product Engineer role: [watch this
video](https://youtu.be/I7i8WabFHcY) or check out
[our blog](https://incident.io/blog/interns-at-incident-io) written by our last
interns to see how it differs from other roles.

We're looking for candidates that:

- Want to work in a fast-paced engineering team in one of London's fastest
  growing start-ups.
- Love the idea of working closely with customers to build a product used daily
  to respond to critical incidents.
- Are excited by the opportunity to build software used by some of the most
  recognisable names in tech: OpenAI, Netflix, Lovable, Linear and more that we
  can't share yet!

We're not looking candidates that:

- Are looking for an 'intern' project: this placement will have you doing
  real work and we'll make little distinction between an intern and a fulltime
  engineering hire.
- Don't enjoy learning new technologies by 'doing': we expect engineers to
  get involved building and learn as they go (most have learned Go while on the
  job, as an example).
- Prefer to work solo: we're highly collaborative and all your work will
  happen as part of a team.

> Pro-tip: you can get a sense of engineering at incident.io by reading our
> [engineering blog](https://incident.io/blog/engineering).

The full candidate process will be:

1. Apply with cover letter
2. If accepted, we'll ask you to provide a solution to our take home test
3. If successful, you'll be invited to an on-site interview — scheduled for November 11th or 13th for interns and placement students, or November 25th or 27th for graduates

## Complete our take-home challenge

### Intro

Imagine you're working at incident.io and we're building a product that can page
(call them, send an SMS, send a notification to a mobile app, etc) engineers
when their services are involved in an incident.

When configuring an on-call system, you don't want to say "whenever service X
goes down, page Y person" as that person probably has a social life and won't
appreciate receiving all the pages, all the time.

Instead, you want to build schedules: a set of people who take it in turns to
provide cover for a service by rotating through on-call shifts.

In JSON form, the configuration that describes how a schedule behaves might look
like this:

```js
// This is a schedule.
{
  "users": [
    "alice",
    "bob",
    "charlie"
  ],

  // 5pm, Friday 7th November 2025
  "handover_start_at": "2025-11-07T17:00:00Z",
  "handover_interval_days": 7
}
```

In that example, our schedule will rotate evenly between those users with the first shift starting at 5pm, 
Friday 7th November 2025, with shift changes happening every 7 days.

That means:

- Alice takes the shift for 1 week, starting at 5pm, Friday 7th November 2025
- Then Bob is on-call for 1 week from 5pm, Friday 14th November 2025
- Then Charlie, then...
- Back to Alice again.

Visually, this might look like this:

![Schedule](./schedule2025.png)

Schedule systems often support 'overrides' where you can add temporary shift
modifications to a schedule, such as if someone wants to go walk their dog or go
to the cinema.

An override specifies the person that will take the shift and the time period it covers.
An example of Charlie covering 5pm–10pm on Monday 10th November 2025 would look like this:

```js
// This is an override.
{
  // Charlie will cover this shift
  "user": "charlie",
  // 5pm, Monday 10th November 2025
  "start_at": "2025-11-10T17:00:00Z",
  // 10pm, Monday 10th November 2025
  "end_at": "2025-11-10T22:00:00Z"
}
```

You can assume that overrides will always be after the schedule's `handover_start_at`, and won't 
overlap with each other.

### Task

We would like you to build – in any language you choose, but ideally one you are
very comfortable in – a script called `./render-schedule` that implements a
scheduling algorithm.

It should be run like so:

```console
$ ./render-schedule \
    --schedule=schedule.json \
    --overrides=overrides.json \
    --from='2025-11-07T17:00:00Z' \
    --until='2025-11-21T17:00:00Z'
[
  {
    "user": "alice",
    "start_at": "2025-11-07T17:00:00Z",
    "end_at": "2025-11-10T17:00:00Z"
  },
  {
    "user": "charlie",
    "start_at": "2025-11-10T17:00:00Z",
    "end_at": "2025-11-10T22:00:00Z"
  },
  {
    "user": "alice",
    "start_at": "2025-11-10T22:00:00Z",
    "end_at": "2025-11-14T17:00:00Z"
  },
  {
    "user": "bob",
    "start_at": "2025-11-14T17:00:00Z",
    "end_at": "2025-11-21T17:00:00Z"
  }
]
```

Where:

- `--schedule` JSON file containing a definition of a schedule (see above example)
- `--overrides` JSON file containing an array of overrides (see above example)
- `--from` the time from which to start listing entries
- `--until` the time until which to list entries

The script should output a JSON array of final schedule as a list of entries.
This should take into account the projected entries (based on the handover
information in the schedule) alongside the provided overrides.

Your schedule should also be truncated based on the from and until parameters provided. 
For example, if an entry was from 1pm November 7 → 1pm November 9, 
but from was 2pm November 8, the entry should be returned as 2pm November 8 → 1pm November 9 
(ignoring the part of the entry that is outside the provided range).

Entries should be truncated to match the from/until parameters.

We care more about correctness than performance: we will only run your code for
time windows up to a few weeks, and with under 100 overrides.

### Code submission and video explanation

We'd like you to submit two things:
1. Your code
2. A 5-minute video walkthrough

Please submit a ZIP file containing the code and a `README.md` that includes 
instructions on running your code, including installation of dependencies.

In the 'notes' field, include a link to a 5-minute video explaining:
- How you approached solving the problem, and why you chose that approach
- How your code implements that solution
- Now you've built the scheduler, what other product features might you build
  on top of this

Imagine you're showing this code to a new team-mate: your video should get
them up-to-speed on the codebase.

(We recommend [Loom](https://www.loom.com) for recording this, but you're welcome 
to use any other tool you're comfortable with).
