Metamap-Gate-Wrapper
========================

<b>This component is a Gate wrapper of the Metamap application.  Could be easily downloaded and run as a docker container.
</b> 

Metamap-gate-wrapper is a system that can be build and run as a docker container, which objective is to easily map the UMLS Terminology to a Gate file using the METAMAP API and the Tagger_MetaMap Gate plugin.
 

MetaMap 
=================================


MetaMap, from the National Library of Medicine (NLM), maps biomedical text to the UMLS Metathesaurus and allows Metathesaurus concepts to be discovered in a text corpus.

The metamap-gate-wrapper can be build and run as a docker container.  Uses the MetaMap plugin for GATE which wraps the MetaMap Java API client to allow GATE to communicate with a remote (or local) 
MetaMap PrologBeans mmserver18 and MetaMap distribution. This allows the content of specified annotations (or the entire document content) to be processed by MetaMap and the results converted to GATE annotations and features. 

The idea is to build and execute the metamap-gate-wrapper as a software container. A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system agents, system libraries and settings.

To use this system, you will need access to a remote MetaMap server, or install one locally by downloading and installing the complete distribution:

http://metamap.nlm.nih.gov/

and Java PrologBeans mmserver

http://metamap.nlm.nih.gov/README_javaapi.html

Requiered:

A Metamap Server running in the host machine. 

It's recomended that the server uses the default port 8066. 

For more information go to the Metamap oficial page: 
https://metamap.nlm.nih.gov/

Tagger_MetaMap Gate plugin:
https://gate.ac.uk/gate/plugins/Tagger_MetaMap/

Parameters 
=================================

-i Input Directory

Input folder that contains the Gate files to be processes.

-o Ouput Directory 

Output folder to storage the results of the MetaMap tagging.

-stm Semantic Type Mapping

The component gives the posibility of map the Metastaurus terminology into the labels that the user specify.  Also at the same time provides a way to retrict the semantic type to be search by MetaMap.  For this aim a semantic mapping file has to be provided with this format:

dsyn|T047|Disease or Syndrome|DISEASE
emst|T018|Embryonic Structure|ANATOMY
ffas|T021|Fully Formed Anatomical Structure|ANATOMY
fndg|T033|Finding|FINDING
grup|T096|Group|GROUP

The format and information is a variation of the information provided by METAMAP about the semantic types:

https://metamap.nlm.nih.gov/Docs/SemanticTypes_2018AB.txt 

With this configuration, for example, Disease or Syndrome will be retrieve and the resulting terms will be mapped as DISEASE Annotation.

These agent was build with specific purposes, and not all the Metamap parameters are mapped to the Metamap server.  These will be done in the future, for now default parameters are used.

Docker Build and Running  
=================================

Build and run the docker individually

	# To build the docker, just go into the linnaeus-gate-wrapper folder and execute
	docker build -t metamap-gate-wrapper .
	#To run the docker, just set the input_folder and the output
	mkdir metamap_output;docker run -u $UID --rm -ti --network host -v $PWD/dnorm_output:/in:ro -v $PWD/metamap_output:/out metamap-gate-wrapper metamap-gate-wrapper -i /in -o /out