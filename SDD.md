# Software design document 

This is the Software design document for Source toSource2 reimporter project

- name: Source toSource2 reimporter <!--T3: hehe funny wording sourcetosource2 -->
- shortname: STS2-REIM
- written by: T342guy

# Pre-Overview

> [!TIP]
> Please read this carefully! There are some keywords in here that will help you understand this document better.

- `Source toSource2 reimporter` - This project, and the name of it.
- `Source1` - The Source engine.
- `Source2`, `S2` - The Source 2 engine.
- `ModelDoc` - The model editor used by the Source2 engine, found in the workshop tools. 
- `S2FM`, `S2Filmmaker` - The Source 2 version of the source filmmaker utility. 
  - `SFM` - The Source1 version of Source filmmaker. (this is the original)
- `reimporting`, aka `porting` - (in our case) The process of moving over (a) file(s) to a new format from the old format.


# Overview

The Source toSource2 reimporter project is designed to fix issues within the community pipeline for re-importing (aka "porting") game models from source1 to source2.\
Re-importing models to the Source 2 engine from the Source1 engine is a hassle, and is very complex for newcomers.

This project aims to achieve a few things:
- To reduce the overall number of steps it takes the end user to port a model from Source1 to Source2.
  - "Steps" include, but not up to; any extra steps in ModelDoc and using other programs.
- To make a simple and easyily understood system for newcomers to port models.
- To make it easy for the S2FM community to get models into S2FM, without having to stay in SFM or port the model(s) themselves.
- If errors may ocucor, provide highly detailed information and a small user-sided notice to point them in the right direction. 
  - If the end user put a `.mdl` file in the `.txt` file zone, show an error that would say: "Error! Incorrect file format supplied. Note: Please select the file with the .mdl file extention and try again." 

## Development 
This project needs to do a few things to be able to accomplish its purpose. 

It needs to be able to:
- read the data files of source1 engine formats (e.g. `.mdl`, (`.dmx`?)).
- being able to de-compile source1 engine formats.
- reading and writing source1 and source2 formats.

## Info 
This part of the SDD will take notes on other parts of the project. 

## Notes on Source1 + Source2 formats

<!--T3: .vmdl is the Source 2 engine versions of the format. they are COMPLETELY DIFFERENT FROM SOURCE1!
.mdl, amonsgt others, is the Source 1 engine format. The Source 1 format is much more linear whereas the Source 2 format is much more organised. 
Then also, now discovering that you could tecnically directly transfer .mdl data to .vmdl to be then compiled from ModelDoc may allow us to completely skip the step where we decompile .mdl for an FBX compile.
--> 
Through a bit of digging, it has become apparent that we CAN translate the Source1 format to Source2 format. 
We can take the equal type of file, and find their equal pointer in both files. Some need to be re-formatted or adjusted, though this wont be a problem once we figure it out.

Also, fortunately, both versions of `.mdl` and `.vmdl` file's text format has been documented in the VALVe Developer Community wiki.
- https://developer.valvesoftware.com/wiki/VMDL 
- https://developer.valvesoftware.com/wiki/MDL


## Methods of porting 

So, currently this project isnt well equiped on how we are going to do the project. Though, there are ideas.

WIP


# LEGACY IDEAS 

<!--T3: Use this in every one as a reminder, plus add [LEGACY IDEA] to the label of every one. 
> [!CAUTION]
> This is a legacy idea! it may be severely outdated, wrong in scope, or other. 
--> 

> [!NOTE] 
> These legacy ideas are here for history of the project, and are currently for past referance. THESE ARE NOT CURRENT!


## [LEGACY IDEA] If we were to do `.mdl` --> FBX 

> [!CAUTION]
> This is a legacy idea! it may be severely outdated, wrong in scope, or other. 

1. find parts of the Crowbar decompiler that reads and decompiles the source models and textures, then tracing how it does it so we can make our own workflow.
2. find parts of other tools or create ourselves to correctly format these decompiled assets into compileable FBX. <!--T3: This part, yes, I think will need to be ESSENTIAL for this project to be any better then crowbar. otherwise its just a worse version of it. or, skeleton of it. This would atleast be a viable tool to skip crowbar and (perhaps) blender for the acctual compile-for-FBX part. -->
3. compile for FBX
4. by now, the model should be fully textured and modeled, with the bones also fully intact. <!--T3: This part I will assume be the hardest pain in the ass to figure out, since source models and FBX are different in every way. Source models (atleast how they are formatted) have so many possibilities that itll be a PAIN for every single type of way they are formatted to be compatible. -->
5. this should be able to be dropped and exported from ModelDoc. 

> [!WARNING]
> Corrections here: The last step, step 4 and 5 above are WRONG.\
> with FBX, they are usally larger then intended, and you need to scale by 0.4 for them to be correct. (they get smaller)\
> Then also, you would need to MANUALLY add the textures and other things. 

## [LEGACY IDEA] If we were to do `.mdl` --> `.vmdl` 

> [!CAUTION]
> This is a legacy idea! it may be severely outdated, wrong in scope, or other. 

In notes below this, tecnically we can translate directly to `.vmdl`. And yes, this would be a better option then if we were to take the `.mdl` --> FBX --> `.vmdl` route.\
However, this comes with potental drawbacks. First of all, old pointers and new pointers between the 2 files may not be easily migrated with this method.\
This could possibly be solved by doing the `.mdl` --> FBX --> `.vmdl` route, as then they would automatically be re-created. again, this would cause extra steps, more spots of failure, and so fourth.