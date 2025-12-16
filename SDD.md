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

- read the data files of source-format models and textures. There may be mulitple types.
- being able to de-compile them.
- reading decomp models.
- correctly re-assembling them for an FBX import.
- then hopefully correctly reassembled for the final ModelDoc build and export.

This is a mouthful to achive, though we can do a few things to find what we need. 
1. find the parts of the Crowbar decompiler that reads and decompiles the source models and textures <!--T3: I want to be able to take the existing source code of Crowbar (only the parts i need) and create action bindings that will allow me to use the existing system. That way we dont need to do it ourselves. -->
2. find parts of other tools or create ourselves to correctly format these decompiled assets into compileable FBX. <!--T3: This part, yes, I think will need to be ESSENTIAL for this project to be any better then crowbar. otherwise its just a worse version of it. or, skeleton of it. This would atleast be a viable tool to skip crowbar and (perhaps) blender for the acctual compile-for-FBX part. -->
3. compile for FBX
4. by now, the model should be fully textured and modeled, with the bones also fully intact. <!--T3: This part I will assume be the hardest pain in the ass to figure out, since source models and FBX are different in every way. Source models (atleast how they are formatted) have so many possibilities that itll be a PAIN for every single type of way they are formatted to be compatible. -->
5. this should be able to be dropped and exported from ModelDoc. 

# Requirements 
Source 2 is kinda all over the place between VALVe games, but mostly the exact same.\
But using the more perferred and widely used amongst the S2FM community, Half-life:Alyx, would be the better version of the source workshop tools to use. (paid)\
Though the workshop tools for Source2 are also on Counter strike 2, Dota 2, and (maybe) artifact. (free)

## Development requirements 

- GoLang 

## Other requirements 
1. Download HL:A
2. Go to `properties` --> `DLC` --> select `Half-life:alyx - workshop tools`.
3. wait for it to finish downloading.
4. start the game.
5. apon the popup, select `Launch workshop tools`.
