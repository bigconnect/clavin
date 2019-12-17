CLAVIN
======


CLAVIN (*Cartographic Location And Vicinity INdexer*) is an open source software package for document geotagging and geoparsing that employs context-based geographic entity resolution. It combines a variety of open source tools with natural language processing techniques to extract location names from unstructured text documents and resolve them against gazetteer records. Importantly, CLAVIN does not simply "look up" location names; rather, it uses intelligent heuristics-based combinatorial optimization in an attempt to identify precisely which "Springfield" (for example) was intended by the author, based on the context of the document. CLAVIN also employs fuzzy search to handle incorrectly-spelled location names, and it recognizes alternative names (e.g., "Ivory Coast" and "Côte d'Ivoire") as referring to the same geographic entity. By enriching text documents with structured geo data, CLAVIN enables hierarchical geospatial search and advanced geospatial analytics on unstructured data.


How to build & use CLAVIN:
--------------------------

1. Check out a copy of the source code:
	> `git clone https://github.com/Berico-Technologies/CLAVIN.git`

2. Move into the newly-created CLAVIN directory:
	> `cd CLAVIN`

3. Download the latest version of allCountries.zip gazetteer file from GeoNames.org:
	> `curl -O http://download.geonames.org/export/dump/allCountries.zip`

4. Unzip the GeoNames gazetteer file:
	> `unzip allCountries.zip`

5. Compile the source code:
	> `mvn compile`

6. Create the Lucene Index (this one-time process will take several minutes):
	> `MAVEN_OPTS="-Xmx4g" mvn exec:java -Dexec.mainClass="com.bericotech.clavin.index.IndexDirectoryBuilder"`

7. Run the example program:
	> `MAVEN_OPTS="-Xmx2g" mvn exec:java -Dexec.mainClass="com.bericotech.clavin.WorkflowDemo"`
	
	If you encounter an error that looks like this:
	> `... InvocationTargetException: Java heap space ...`
	
	set the appropriate environmental variable controlling Maven's memory usage, and increase the size with `export MAVEN_OPTS=-Xmx4g` or similar.

Once that all runs successfully, feel free to modify the CLAVIN source code to suit your needs.

**N.B.**: Loading the worldwide gazetteer uses a non-trivial amount of memory. When using CLAVIN in your own programs, if you encounter `Java heap space` errors (like the one described in Step 7), bump up the maximum heap size for your JVM.

* Add a dependency on the CLAVIN project:

```xml
<dependency>
   <groupId>com.bericotech</groupId>
   <artifactId>clavin</artifactId>
   <version>2.0.0</version>
</dependency>
```

>  You will still need to build the GeoNames Lucene Index as described in steps 3, 4, and 6 in "How to build & use CLAVIN".

License:
--------

Copyright (C) 2012-2016 Berico Technologies

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
