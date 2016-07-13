1. European Organization 

  This project aims at creating a rdf [1] dataset for major european organizations using W3C's Organization Ontology [2].
  It can be considered preparatory work for a project to triplify the CETA Treaty [3].
  
2. Notes on the dataset
  1. Actual Organizations of the European Union are typed org:FormalOrganization [4]
  2. As of now countries are typed org:Organization [5]
  3. The relation between an organization and a country is expressed using an org:Membership [6] construct. See also the example under "Membership n-ary relationship" here [7]
  4. URIs follow the below schemes.
    1. Countries<br/>
    ${baseURL}/${dataset-identifier}/${ISO 3166-1 alpha-2} , e.g.<br/>
    http://organization.turnguard.com/europe/at (=URI for Republic of Austria)
    2. Organizations<br/>
    ${baseURL}/${dataset-identifier}/${unofficial-shortcut} , e.g.<br/>
    http://organization.turnguard.com/europe/eu (=URI for European Union)
    3. Memberships<br/>
    ${baseURL}/${dataset-identifier}/${unofficial-shortcut}/${ISO 3166-1 alpha-2} , e.g.<br/>
    http://organization.turnguard.com/europe/eu/at (=URI for Republic of Austria's membership in the European Union)
  5. Dates and times<br/>
    Dates and times are given in xsd:dateTime [8] and UTC [9]. DateTimes were converted using this tool [10]. For instance, the Republic of Austria is a European Union member since 01.01.1995, if not explicitly stated, 00:00 is assumed, which is then translated into UTC, giving 1994-12-31T23:00:00Z. All intervals (e.g. the duration of a membership within an organization are expressed using W3C's Time Ontology [11].
  6. Metadata<br/>
    A dcterms:title [12] relation in english is available for entity description where it makes sense (e.g. not for memberships). The rdfs:comment [13] predicate is used to state clarifications where necessary. The rdfs:seeAlso [14] predicate is used to point to other resources or entity descriptions on the web.
  7. The whole dataset is licenced under
     http://creativecommons.org/licenses/by-sa/3.0/
  8. Sample Queries<br/>
    1. The European Union (on sparql.turnguard.com/sparql : http://goo.gl/A49ihw)<br/>
    ```
    SELECT * 
      FROM <http://organization.turnguard.com/europe>
      WHERE {
        <http://organization.turnguard.com/europe/eu> ?p ?o
    }
  ```
    2. Members of the European Union (+since when) (on sparql.turnguard.com/sparql : http://goo.gl/zTBMgQ)<br/>
    ```
    PREFIX org:<http://www.w3.org/ns/org#>
    PREFIX time:<http://www.w3.org/2006/time#>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    SELECT
      ?country
      ?memberSince
    FROM <http://organization.turnguard.com/europe>
    WHERE {
      ?membeship org:organization <http://organization.turnguard.com/europe/eu>;
                 org:member/dcterms:title ?country;
                 org:memberDuring/time:hasBeginning/time:inXSDDateTime ?memberSince
    } ORDER BY DESC(?memberSince)
  ```

&nbsp;&nbsp;[1] https://www.w3.org/TR/rdf11-primer/<br/>
&nbsp;&nbsp;[2] https://www.w3.org/TR/vocab-org<br/>
&nbsp;&nbsp;[3] http://ec.europa.eu/trade/policy/in-focus/ceta/<br/>
&nbsp;&nbsp;[4] https://www.w3.org/TR/vocab-org/#class-formalorganization <br/>
&nbsp;&nbsp;[5] https://www.w3.org/TR/vocab-org/#org:Organization<br/>
&nbsp;&nbsp;[6] https://www.w3.org/TR/vocab-org/#class-membership<br/>
&nbsp;&nbsp;[7] https://www.w3.org/TR/vocab-org/#reporting_structure<br/>
&nbsp;&nbsp;[8] https://www.w3.org/TR/xmlschema-2/#dateTime<br/>
&nbsp;&nbsp;[9] https://en.wikipedia.org/wiki/Coordinated_Universal_Time<br/>
[10] http://www.timeanddate.com/worldclock/converter.html<br/>
[11] https://www.w3.org/TR/owl-time/<br/>
[12] http://dublincore.org/documents/dcmi-terms/#terms-title
[13] https://www.w3.org/TR/rdf-schema/#ch_comment
[14] https://www.w3.org/TR/rdf-schema/#ch_seealso
