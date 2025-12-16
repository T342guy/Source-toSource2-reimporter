# Software design document 

This is the Software design document for Source toSource2 reimporter 

- name: Source toSource2 reimporter <!--T3: hehe funny wording sourcetosource2 -->
- shortname: STS2-REIM
- written by: T342guy

# Project 

The Source toSource2 reimporter project is designed to fix some issues within the pipeline for re-importing models to Source2. 

Re-importing models to the Source 2 engine from the OG Source engine is a hassle. And, it is very complex for those just getting to know this. 

So, this project aims to do a few things: 
- To reduce the overall number of steps it takes for a model from Source to be compatible with Source2. Even going as far to see if it is possible to compile the model for S2 directly. (though unlikely)
- To make it easy, and increase the workflow for those wanting to use S2fimaker more often then being handikapped to SFM since model support is insufficent in S2FM.
- Being an easy to know tool for experienced and newcomers alike.

# Development 
This project needs to do a few things to be able to accomplish its purpose. 

It needs to be able to:
- read the data files of source-format `.mdl` models and textures. There may be mulitple types, and versions.
- being able to de-compile `.mdl` format models.
- reading the raw format models.
- correctly re-assembling raw format for FBX.
- then hopefully correctly reassembled correctly. 
- read and write the `.vmdl` format for self-checking and acctually making the new file. 
- Read and write the FBX format.
- Downscale the FBX model automatically by .4 since its some sorta bug with FBX.

## If we were to do `.mdl` --> FBX 

1. find parts of the Crowbar decompiler that reads and decompiles the source models and textures, then tracing how it does it so we can make our own workflow.
2. find parts of other tools or create ourselves to correctly format these decompiled assets into compileable FBX. <!--T3: This part, yes, I think will need to be ESSENTIAL for this project to be any better then crowbar. otherwise its just a worse version of it. or, skeleton of it. This would atleast be a viable tool to skip crowbar and (perhaps) blender for the acctual compile-for-FBX part. -->
3. compile for FBX
4. by now, the model should be fully textured and modeled, with the bones also fully intact. <!--T3: This part I will assume be the hardest pain in the ass to figure out, since source models and FBX are different in every way. Source models (atleast how they are formatted) have so many possibilities that itll be a PAIN for every single type of way they are formatted to be compatible. -->
5. this should be able to be dropped and exported from ModelDoc. 

Corrections here: The last step, step 4 and 5 above are WRONG. with an FBX they are usally larger then intended, and you need to scale by 0.4 for them to be correct.\
Then also, you would need to MANUALLY add the textures and other things. 

## If we were to do `.mdl` --> `.vmdl` 
In notes below this, tecnically we can translate directly to `.vmdl`. And yes, this would be a better option then if we were to take the `.mdl` --> FBX --> `.vmdl` route.\
However, this comes with potental drawbacks. First of all, old pointers and new pointers between the 2 files may not be easily migrated with this method.\
This could possibly be solved by doing the `.mdl` --> FBX --> `.vmdl` route, as then they would automatically be re-created. again, this would cause extra steps, more spots of failure, and so fourth.

## Possible ways to do this. 

<!--T3: .vmdl and .vmdl_c are the Source 2 engine versions of the format. they are COMPLETELY DIFFERENT. 
The .mdl and (maybe) .mdl_c are the Source 1 engine formats. The Source 1 format is much more linear whereas the Source 2 format is much more organised. 
Then also, now discovering that you could tecnically directly transfer .mdl data to .vmdl to be then compiled from ModelDoc may allow us to completely skip the step where we decompile .mdl for an FBX compile.
--> 
There is no direct way to easily and simply make a `.vmdl_c` file. A `.vmdl_c` file is the game-side binary compiled version of the model.\
We can, however, create a `.vmdl` file. The `.vmdl` file is the content-side text version of the encoded model that ModelDoc can read and finally compile into a `.vmdl_c`.\

Also, fortunately, both versions of `.mdl` and `.vmdl_c` file's text format has been documented in the VALVe Developer Community wiki.\
- https://developer.valvesoftware.com/wiki/VMDL 
- https://developer.valvesoftware.com/wiki/MDL

# Requirements 
Source 2 is kinda all over the place between VALVe games, but mostly the exact same.\
But using the more perferred and widely used amongst the S2FM community, Half-life:Alyx, would be the better version of the source workshop tools to use. (paid)\
Though the workshop tools for Source2 are also on Counter strike 2, Dota 2, and (maybe) artifact. (free)

## Development requirements 

- GoLang 

## Other requirements 
Source 2 workshop tools; (can use CS2 aswell)
1. Download HL:A
2. Go to `properties` --> `DLC` --> select `Half-life:alyx - workshop tools`.
3. wait for it to finish downloading.
4. start the game.
5. apon the popup, select `Launch workshop tools`.
