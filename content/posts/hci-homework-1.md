+++
title = "HCI Homework 1: Affordances, Gestalt Laws, and Dark Patterns"
date = 2026-09-18
description = "Three short observations about how everyday interfaces guide, confuse, or manipulate people."
tags = ["HCI", "affordance", "gestalt", "dark patterns"]
categories = ["HCI"]
courses = ["HCI"]
+++

This homework looks at three ways design affects behaviour: the actions an object suggests, the visual groups people perceive, and the choices an interface tries to steer.

> **Submission note:** the two door photographs are openly licensed reference images. For a strictly first-hand submission, I would replace them with photographs taken in the exact places I use every day.

## Lecture 1 - Affordances

An affordance is a quality of an object that suggests how it can be used. A good affordance reduces the need for written instructions.

### Good example: a crash bar on an exit door

![A school exit door with a horizontal crash bar.](/images/hci/homework-1/crash-bar-door.jpg)

*Figure 1. A horizontal crash bar suggests “push here” through its size, position, and direction. Photo by Scott Brody, [CC BY-SA 4.0](https://commons.wikimedia.org/wiki/File:Set_of_Crash_Bar_Doors.jpg).*

The wide horizontal bar sits exactly where a person naturally places their hands or body when leaving. Pushing it is easy, even when carrying something or moving quickly. The physical form matches the intended action, so the sign is only a confirmation rather than the main instruction.

### Bad example: a pull-looking handle on a push door

![A door with push and pull signs.](/images/hci/homework-1/push-pull-door.jpg)

*Figure 2. A door whose handles and signs create a push/pull decision. Photo by Robert S. Donovan, [CC BY 2.0](https://commons.wikimedia.org/wiki/File:Door_with_both_push_and_pull_signs.jpg).*

A long vertical handle invites people to pull. If that handle is placed on the side that must be pushed, the object and the instruction disagree. People stop, read, and often try the wrong action first.

**Redesign:** use a flat push plate on the push side and a handle only on the pull side. The door should communicate its action before a person reads a label.

## Lecture 2 - Gestalt Laws

Gestalt laws describe how people visually group elements. The following cases show what happens when that grouping is not supported by the layout.

### 1. Proximity: shelf labels that appear to belong to the wrong product

![A public-domain diagram demonstrating the Gestalt law of proximity.](/images/hci/homework-1/gestalt-proximity.png)

*Figure 3. Elements placed close together are perceived as a group. Public-domain diagram from [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Gestalt_proximity.svg).*

On a crowded supermarket shelf, price labels can be placed midway between two product columns. A shopper then groups a price with the closest package, even when it belongs to the product beside it. The result is uncertainty at the shelf and frustration at checkout.

**Correction:** align each label directly under its product, preserve a consistent vertical column, and add more space between product groups than within a group.

### 2. Similarity: identical controls with different consequences

In a self-service machine, a large row of identical grey buttons may include *Pay*, *Cancel*, *Back*, and *Print*. Because colour, size, and shape are the same, users perceive them as equally safe actions. A destructive action such as *Cancel* can be pressed by mistake.

**Correction:** keep related navigation controls visually similar, but make the primary action prominent and separate destructive actions with a warning colour, a different position, and enough empty space. Similar appearance should mean similar consequences.

## Lecture 3 - Dark Design Patterns

Dark patterns use wording, hierarchy, or friction to make the company-preferred choice easier than the user-preferred choice. Nielsen Norman Group describes these patterns as designs that deceive, misdirect, shame, or obstruct people when they try to choose otherwise.

### 1. Confirmshaming in a newsletter popup

A popup may offer two choices: a large button saying **“Yes, send me the discount”** and a small link saying **“No thanks, I do not like saving money.”** The second option makes declining feel irrational or embarrassing. The wording is not neutral; it pressures the user emotionally.

**Opposite redesign:** use two equally visible, factual choices: **“Subscribe to the newsletter”** and **“No thanks.”** State the benefit and frequency of emails before either button. The user can then decide without shame.

### 2. Obstructive subscription cancellation

Some services make sign-up one click but place cancellation behind several account screens, retention offers, and repeated confirmation questions. The extra steps increase the cost of leaving rather than helping the user make an informed choice.

**Opposite redesign:** show **“Cancel subscription”** clearly in the subscription settings, explain the end date and effect once, and confirm the cancellation on the next screen. Leaving should be as understandable as joining.

## Sources

- [Door with push and pull signs - Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Door_with_both_push_and_pull_signs.jpg)
- [Crash-bar door photograph - Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Set_of_Crash_Bar_Doors.jpg)
- [Gestalt proximity diagram - Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Gestalt_proximity.svg)
- [Deceptive Patterns in UX - Nielsen Norman Group](https://www.nngroup.com/articles/deceptive-patterns/)
- [Stop Shaming Your Users for Micro Conversions - Nielsen Norman Group](https://www.nngroup.com/articles/shaming-users/)
