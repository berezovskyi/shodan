# shodan

An [event-sourcing-based](http://martinfowler.com/eaaDev/EventSourcing.html) RDF datastore and processor.

## Usage

Let's create a new RDF datastore first:

	$ python shodan.py --init ex1
	2012-09-17T04:27:23 INFO Creating new store [ex1]
	2012-09-17T04:27:24 DEBUG Initialised datastore in [/Users/michael/ex1]
	
You can check if this has worked out: go to your home directory where you should find a new directory named with the store name, `ex1` in our case.

Now, lets add some triples. Shodan assumes you have the data in [RDF NTriples](http://www.w3.org/TR/rdf-testcases/#ntriples "RDF Test Cases") format in a file. I'm going to use the [test data](https://github.com/mhausenblas/shodan/tree/master/data) supplied with shodan and go like:

	$ python shodan.py --add ex1:data/input_data_0.nt
	2012-09-17T04:27:28 INFO Adding data to store [ex1] from input file [data/input_data_0.nt]
	2012-09-17T04:27:28 DEBUG Updated datastore [ex1] with:
	<http://example.org/#m> <http://xmlns.com/foaf/0.1/knows> <http://example.org/#r> .

OK, next we want to query the store. You'd do it as follows (again, using the query provided in [test](https://github.com/mhausenblas/shodan/tree/master/data)):

	$ python shodan.py -q ex1:data/query_0.sparql 
	2012-09-18T08:51:14 INFO Querying store [ex1] with SPARQL query from input file [data/query_0.sparql]
	2012-09-18T08:51:14 DEBUG Executing HDT Jena SPARQL query with:
	SELECT * WHERE { ?s ?p ?o } LIMIT 2
	Triples served: 3
	--------------------------------------------------------------------------------------------------------------
	| s                           | p                                  | o                                       |
	==============================================================================================================
	| <file:///Users/michael/ex1> | <http://purl.org/dc/terms/created> | "\"2012-09-18\""                        |
	| <file:///Users/michael/ex1> | <http://purl.org/dc/terms/creator> | <https://github.com/mhausenblas/shodan> |
	--------------------------------------------------------------------------------------------------------------


## Dependencies

* [HDT](http://www.rdfhdt.org/), download and build [HDT Java](http://code.google.com/p/hdt-java/)
* [git](http://git-scm.com/), asssuming everyone has it installed anyways
* [GitPython](https://github.com/gitpython-developers/GitPython), easy install it

## License

This software is licensed under [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0.html) Software License.