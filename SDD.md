# Software design document 

This is the Software design document for Source toSource2 reimporter 

- name: Source toSource2 reimporter
- codename: SourceSpaghetti
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

1. read the Source files of models and textures.
2. being able to de-compile them
3. reading decomp models
4. correctly re-assembling them for an FBX import
5. then hopefully correctly reassembled for the final ModelDoc render

This is a mouthful to achive, though we can do a few things to find what we need. 
1. find the parts of the Crowbar decompiler that reads and decompiles the source models and textures
2. find parts of other tools or create ourselves to correctly format these decompiled assets into compileable FBX.
3. compile for FBX
4. by now, the model should be fully textured and modeled, with the bones also fully intact.
5. this should be able to be dropped and exported from ModelDoc. 
