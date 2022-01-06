👉 [main article](https://atomate.net/blog/setup-solr-6-x-with-mysql/)

## solrconfig.xml
***./server/solr/collection1/conf/solrconfig.xml***
```
<lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-dataimporthandler-.*\.jar" />

<lib dir="${solr.install.dir:../../../..}/contrib/extraction/lib" regex=".*\.jar" />
<lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-cell-\d.*\.jar" />

<lib dir="${solr.install.dir:../../../..}/contrib/langid/lib/" regex=".*\.jar" />
<lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-langid-\d.*\.jar" />

<lib dir="${solr.install.dir:../../../..}/contrib/velocity/lib" regex=".*\.jar" />
<lib dir="${solr.install.dir:../../../..}/dist/" regex="solr-velocity-\d.*\.jar" />
```

And the following to section <!– Request Handlers
```
<requestHandler name="/dataimport" class="solr.DataImportHandler">
    <lst name="defaults">
      <str name="config">db-data-config.xml</str>
    </lst>
</requestHandler>
```

## Create solr-data-config file
***./server/solr/collection1/conf/solr-data-config.xml***
```
<dataConfig>
<dataSource type="JdbcDataSource"
driver="com.mysql.jdbc.Driver"
url="jdbc:mysql://localhost:3306/db_name"
user="root"
password="password"/>
<document>
<entity name="entity_name"
query="SELECT * FROM TABLE_NAME">
<field column="id" name="id"/>
<field column="name" name="name"/>
</entity>
</document>
</dataConfig>
```

```properties
solr restart -p 8983
```

## Schema.xml
```
<schema name="course_batches" version="1.5">
    <field name="_version_" type="long" indexed="true" stored="true"/>
    <field name="id" type="num" indexed="true" stored="true" required="true" /> 
    <field name="title" type="string" indexed="true" stored="true"/>
</schema>
```