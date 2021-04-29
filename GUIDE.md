# STEP-BY-STEP GUIDE 🗺

Many software engineers struggle with system design interviews (SDIs). This is due to the vague nature inherent to them; they are unstructured, most people don't have experience designing large scale distrubuted systems, and people just flat-out don't spend enought time preparing for them.

## TABLE OF CONTENTS

1. [Step 1: Requirements](#step-1-requirements)
2. [Step 2: Make Some Estimates](#step-2-make-some-estimates)
3. [Step 3: Define the System Interface](#step-3-define-the-system-interface)
4. [Step 4: Define the Data Model](#step-4-define-the-data-model)
5. [Step 5: Make the Meta-Level Design](#step-5-make-the-meta-level-design)
6. [Step 6: Detailed Design](#step-6-detailed-design)
7. [Step 7: Figure Out (and Resolve) Bottlenecks](#step-7-figure-out-and-resolve-bottlenecks)

## STEP 1: REQUIREMENTS

You should always ask questions about the scope of the problem that you're trying to solve. These types of problems are open-ended, and they don't really have a single correct answer.

Get clarifications on ambiguities whenever you can. Getting a clear picture always sets you up for success. Since you will only have 30-45 minutes to design a system, you will need to get clarification on which parts of the system you'll _actually_ be focusing on.

For instance, here's an example of designing a social media system:

1. Will users make posts and follow other people?
2. Should we design to create/display a home timeline?
3. Are we dealing with media (photos, videos, audio)?
4. Is this back-end only, or should we design the front-end as well?
5. Will users be able to search on this platform?
6. Do we have trending topics?
7. Should users receive push notifications?

These aren't a complete list, but this illustrates how we could ask questions that clarify requirements for the interview.

## STEP 2: MAKE SOME ESTIMATES

We should estimate the scale that we're designing. This helps us later when we focus on scaling, partitioning, load balancing, and caching.

1. What scale is expected from the system (number of posts, number of view on the home timeline per second, number of users per day, etc.)?
2. How much storage should we set up? The needs will also be drastically different if the users store various types of media depending on what that media is.
3. What kind of network bandwidth usage should we expect on the system? We'll need to manage traffic and balance load between any of our servers that we design.

## STEP 3: DEFINE THE SYSTEM INTERFACE

## STEP 4: DEFINE THE DATA MODEL

## STEP 5: MAKE THE META-LEVEL DESIGN

## STEP 6: DETAILED DESIGN

## STEP 7: FIGURE OUT (AND RESOLVE) BOTTLENECKS
