# Renov8 - Historical

Our goal is to create a well organized catalog of design aesthetics from the
15th century into the present.

We care about cataloging components by their shape, material, and aesthetic
design characteristics.  Along side an accurate depiction of the design and
historical information should be example imagery.

The goal is to classify which designs and materials were correlated by space and
time.  

The dataset library we curate should be usable to train a simple classifier
which accepts an image of an item and can estimate the place and period of time
it best resembles.

At the end of this we should have stored in the `./library/` directory a well
organized collection of information alongside images that can be used for
training.

It's important that we will be learning the PROPER NAMES for specific design
elements within the images we are curating.  Those proper names should have a
dictionary definition and be properly associated with the images.  

# First Run

On first run, every agent must establish a comms channel with every other
relevant agent as specified later in this document.  After 15 minutes,
re-evaluate the comms channel.  Then after 1 hour, re-evalute.

# Directory layout.

## `./library`

This is the heavily curated and organized data.  The only person who should
modify the files in here should be the librarian.

## `./research-targets`

This should contain a list of things which are worth researching, with a brief
description of what they are for.  It might contain a list of websites to crawl
OR it might contain periods/regions which need to be discovered.

## `./research-findings`

Once information has been crawled, it's quazi-consolidated form should be stored
into the research-findings. 

## `./tools`

If you need to write scripts to parse data such as YAML, JSON, or HTML - write
them as python programs and use the venv in that directory.  Feel free to update
the requirements.txt as needed.

If an agent requires a tool to be built.  They should drop a specification with
examples in a SPEC subdirectory within there.

# Context

Our goal is to be minimimizing our context window, with perhaps exception to the
librarian.  Agents should store near their override file a `.context/` directory
which is checkpointed by broader topic.  

This allows them to save relevant context while dismissing it for their current
operations which may not be relevant.

# Communication

Feel free to use any communication form you wish, pure english is not necessary
or even ideal in all cases when communicating.  Prefer to be as terse as
possible to minimize wasted token usage.

Please feel free to negotiate comms languages which minimize total tokens.  It
need not even be a true language, only a computational form to express intent
accurately.  Language is not always the ideal transform for information... even
if you need a referential language dictionary.

You should have a communication channel with EVERY OTHER AGENT which exists,
even if you do not need much from them.  It should be append only files which
demarcate the SENDER / RECEIVER.  And the communications should reside in the
`.comms/` directory.  

Something like:
- `.comms/acquisition-engineer.txt` (for reciprocal acquisition to engineer 
  communication)
- `.comms/librarian-researcher.txt` (for reciprocal researcher librarian
  communication)

Periodically compact the comms when tasks are done and rotate the messages.
Clear context window if you were performing rote tasks.

# Priorities

We care mostly about elements which *still* exist in modern homes.
- Furniture
- Lamps
- Sink basins
- Faucets
- Bathtubs
- Vanities
- Paint
- Wallpaper
- Curios
- Credenzas

The librarian and researcher should collaborate on a common list of items to
consider and share it in `research-targets/OBJECTIVE_FURNISHINGS.md`.

They should also partition this information by period and geography.  Targeting
specific periods and geographies coordinated.

# Agents

The root agent is responsible periodically poking the agents and encouraging
them to act.

## acquisition

The voracious reader.

Model: qwen-medium (REQUIRED/PREFERRED)
Use Qwen for source triage, browser extraction, packet drafting, and
acquisition handoffs. Do not silently substitute another model.
Directory: ./agents/acquisition

## engineer

The builder of tools.

Model: 
- qwencode-high (REQUIRED/PREFERRED)
- terra-medium (If necessary)
Use Qwen Coder for implementation and review whenever available; use Terra
only when Qwen Coder is unavailable.
Directory: ./agents/engineer


## librarian

The diligent perfectionist.

Model: 
- sol-medium (HIGHLY PREFERRED)
- sol-high (If necessary)
Qwen may perform low-cost extraction or pre-review, but Sol remains the final
curation/reconciliation model unless explicitly changed.

Directory: ./agents/librarian

## researcher

The curious cynic excited to learn.

Model: luna-medium
Directory: ./agents/researcher

## visual-interpreter

The visual image feature interpreter.

Model:
- qwen-medium (REQUIRED first pass; minimize downstream token usage)
- sol-medium (Only for Qwen-flagged ambiguity or required deep review)
- sol-high (If necessary)
Never send an image to Sol before a Qwen first pass.

Directory: ./agents/visual-interpreter
