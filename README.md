## XML Concepts
# What is XML?
•	XML stands for extensible Markup Language. It’s a markup language like HTML – it has open and closing tags with specific meanings.
•	XML lets us define our own markup elements, it was conceived because of hardware and software in the past being unable to exchange data.
### Example
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;note&gt;
  &lt;to&gt;Tove&lt;/to&gt;
  &lt;from&gt;Jani&lt;/from&gt;
  &lt;heading&gt;Reminder&lt;/heading&gt;
  &lt;body&gt;Don't forget me this weekend!&lt;/body&gt;
&lt;/note&gt;
Note: The xml declaration at the top is optional
XML Validator
XML files can be validated using an XML schema from on XSD file (another type of XML file)
An XML file is well-formed provided that:
•	There is a root document. I.e., there is an enclosing tag around all elements
•	Each open tag is closed and are case sensitive.
•	Attribute values are quoted (single or double)
•	Elements are properly nested (it may be illegal to have a specific nesting pattern)
Where is XML used?
•	Used to represent configuration files (e.g., pom.xml)
•	Storing and manipulating data
XML Processor
What is an XML Processor?
This is software which can read XML. It can store the XML’s data as in-memory structures which then can be accessed by a program. It checks for validation and well-formedness
What is an XML Parser?
This is also an XML processor which represents XML in a format which can be used by a programming language. E.g., Java has several XML parsers such as SAX, STAX etc 
 
XML Instances
What is an XML instance?
•	This is an XML file with extension .xml which contains data.
•	In version 1.1 of XML recommendation, an XML declaration is required at the top of the XML file
XML Declaration
&lt;?xml version="1.0" encoding="UTF-8" standalone="no"?&gt;

•	The encoding attribute is a facet which determines the valid character set for the XML file.
o	It’s default value of UTF-8 but can also be set to UTF-16 which has a wider valid space of characters
•	The standalone attribute is a facet which indicates if an external XML file is needed to process the XML. For example, we may have an XML schema for validation
o	 Its default value is “no”
Elements
•	Elements of an XML file are components which are wrapped with an opening and closing tag
o	E.g., &lt;Message&gt;Hello World&lt;/Message&gt;
•	The name of elements is an XML non-colonised name (cannot contain a colon)
•	Can start with either a letter or underscore (_)
•	Can contain letters, digits, hyphens (-), periods (.) and underscores (_)
•	Cannot contain special characters like whitespace, ?, *, /, … etc
Root Element
•	All valid XML files have a root element
•	This is the enclosing element tag of all child elements
Child Elements
•	We may have elements within other elements. 
•	E.g.
&lt;ParentElement&gt;
	&lt;Child1&gt;&lt;/Child1&gt;
	&lt;Child2&gt;&lt;/Child2&gt;
	&lt;Child3&gt;&lt;/Child3&gt;
&lt;/ParentElement&gt;

Attributes
•	Attributes are also knowns as facets
•	They provide additional data to an element
•	We could use an attribute to provide a link to an entity
 
XML Schemas
What is an XML Schema?
•	Schemas define the blueprint of an XML file, its an XML file itself but with extension .xsd
•	If we wanted to restrict how an XML file is composed, we validate it against a schema.
Purpose of Schemas
•	Verification and validation of XML documents
•	Control properties such as:
o	Attributes
o	Order of elements
o	Uniqueness of values
o	Restrict data values to enumeration, ranges, and patterns
•	Schemas act as a contract for valid XML instances
•	Aids XML processors to effectively process XML data
Example
Product.xsd:
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"&gt;
	&lt;xs:element name="product" type="ProductType" /&gt;
	&lt;xs:complexType name="ProductType"&gt;
		&lt;xs:sequence&gt;
			&lt;xs:element name="number" type="xs:integer" /&gt;
			&lt;xs:element name="size" type="SizeType" /&gt;
		&lt;/xs:sequence&gt;
		&lt;xs:attribute name="effDate" type="xs:date" /&gt;
	&lt;/xs:complexType&gt;
	&lt;xs:simpleType name="SizeType"&gt;
		&lt;xs:restriction base="xs:integer"&gt;
			&lt;xs:minInclusive value="2" /&gt;
			&lt;xs:maxInclusive value="18" /&gt;
		&lt;/xs:restriction&gt;
	&lt;/xs:simpleType&gt;
&lt;/xs:schema&gt;

Product.xml:
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;product effDate="2001-04-12"&gt;
	&lt;number&gt;557&lt;/number&gt;
	&lt;size&gt;10&lt;/size&gt;
&lt;/product&gt;





 
XML Schema Definitions: Simple Types
Simple and Complex types
•	To get a grasp of how to define XML schemas we need to understand what exactly simple types and complex types are
•	Elements of an XML instance can either be of simple or complex type
Simple Type
•	Have a no child elements and do not have attributes
•	We can distinguish simple types further to
1)	Atomic Types: values which are indivisible. E.g., &lt;size&gt;10&lt;/size&gt;
2)	List Types: whitespace separated atomic values. E.g., &lt;size&gt; 10  Large  M &lt;/size&gt;
3)	Union Types: This is a type which has a valid space of two or more simple types. E.g., if we had a simple type with a range of 2-10 and another with S|R|L, then a simple type of these two combined would yield a union type
Examples:
&lt;size&gt;10&lt;/size&gt;
&lt;comment&gt;Runs large.&lt;/comment&gt;
&lt;availableSizes&gt;10 large 2&lt;/availableSizes&gt;

&lt;size system="US-DRESS"&gt;10&lt;/size&gt;
&lt;comment&gt;Runs &lt;b&gt;large&lt;/b&gt;.&lt;/comment&gt;
&lt;availableSizes&gt;&lt;size&gt;10&lt;/size&gt;&lt;size&gt;2&lt;/size&gt;&lt;/availableSizes&gt;

Complex Type
•	A complex type may have child attributes and/or attributes
•	We can distinguish Complex Types into four categories:
1)	Simple Content: there are no child elements but the type allows for attributes
Example:
&lt;size system="US-DRESS"&gt;10&lt;/size&gt;
2)	Empty Content: No child elements and no text. Only has attribute
Example:
&lt;picture src="servername/filename"&gt;&lt;/picture&gt;
3)	Element-Only Content: Child elements defined but no character data within parent element itself (only within child elements)
Example:
&lt;product&gt;
	&lt;number&gt;557&lt;/number&gt;
	&lt;name&gt;Short-Sleeved Linen Blouse&lt;/name&gt;
	&lt;size system="US-DRESS"&gt;10&lt;/size&gt;
	&lt;color value="blue" /&gt;
&lt;/product&gt;
4)	Mixed Content: Child elements with intermingled characters in parent element
Example:
&lt;desc&gt;This is our &lt;i&gt;best-selling&lt;/i&gt; shirt.
 &lt;b&gt;Note: &lt;/b&gt; runs &lt;u&gt;large&lt;/u&gt;.&lt;/desc&gt;

•	We have the ability to constrain our XML files to fit into these content models
 
Built in Simple Types
•	There are 49 built-in simple types in the XML schema recommendation.
•	Things like strings, dates, numbers are represented by the simple types
Summary
Category	Built-in-types
Strings and names	string, normalizedString, token, Name, NCName, QName, language
Numeric	float, double, decimal, integer, long, int, short, byte, positiveInteger, nonPositiveInteger, negativeInteger, nonNegativeInteger, unsignedLong, unsignedInt, unsignedShort, unsignedByte
Date and Time	duration, dateTime, date, time, gYear, gYearMonth, gMonth, gMonthDay, gDay, 1.1 dayTimeDuration, 1.1 yearMonthDuration, 1.1 dateTimeStamp
XML DTD types	ID, IDREF, IDREFS, ENTITY, ENTITIES, NMTOKEN,
NMTOKENS, NOTATION
Other	boolean, hexBinary, base64Binary, anyURI

 
Creating Simple Types
Named and Anonymous Types
•	A named type is a type which has a name and is defined globally:
&lt;xs:element name="Dress" type="tns:SizeType" /&gt;
&lt;xs:simpleType name="SizeType"&gt;
	&lt;xs:restriction base="xs:integer"&gt;
		&lt;xs:minInclusive value="2" /&gt;
		&lt;xs:maxInclusive value="18" /&gt;
	&lt;/xs:restriction&gt;
&lt;/xs:simpleType&gt;

Named type instance:
&lt;tns:product xmlns:tns="shivkumar.org/named"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="shivkumar.org/named NamedSimpleType.xsd "&gt;
	&lt;Dress&gt;2&lt;/Dress&gt;
&lt;/tns:product&gt;


•	An anonymous simple type is defined locally of the element using it
&lt;element name="Dress"&gt;
	&lt;!-- Anonymous simple type: --&gt;
	&lt;simpleType&gt;
		&lt;restriction base="integer"&gt;
			&lt;minInclusive value="2" /&gt;
			&lt;maxInclusive value="20" /&gt;
		&lt;/restriction&gt;
	&lt;/simpleType&gt;
&lt;/element&gt;
	
	Anonymous type instance:
	&lt;element name="dress"&gt;
	&lt;!-- Anonymous simple type: --&gt;
	&lt;simpleType&gt;
		&lt;restriction base="integer"&gt;
		      &lt;minInclusive value="2" /&gt;
		      &lt;maxInclusive value="20" /&gt;
	      &lt;/restriction&gt;
	&lt;/simpleType&gt;
&lt;/element&gt;
 
Simple Type Restrictions
•	Every simple type is a restriction of another simple type – we are also able to extend simple types to other simple types
•	You will typically see restrictions having a base type of an inbuilt type (e.g., strings, number…) but you can also have a user defined base type
•	If we are using a user-defined simple type, we must be aware that the restriction MUST restrict the valid space and NOT extend it
Example: Restriction with in-built base type
&lt;!-- Creating a named simple type for demonstration purposes: --&gt;
&lt;simpleType name="IntegerRestriction100"&gt;
	&lt;!-- Restriction on numerical types --&gt;
	&lt;restriction base="integer"&gt;
		&lt;minInclusive value="0" /&gt;
		&lt;maxInclusive value="100" /&gt;
	&lt;/restriction&gt;
&lt;/simpleType&gt;

&lt;element name="numberRange" type="tns:IntegerRestriction100" /&gt;

•	In this example we have a base which is of the inbuilt type “integer”
•	So, our instance could be: 
&lt;tns:numberRange&gt;20&lt;/tns:numberRange&gt;

Example: Restriction with user-defined base type
&lt;element name="numberRangeRestriction"&gt;
	&lt;simpleType&gt;
	&lt;!-- We can also use user-defined types for the base value --&gt;
		&lt;restriction base="tns:IntegerRestriction100"&gt;
		&lt;!-- The restrictions must restrict the valid space of      the base type --&gt;
			&lt;maxExclusive value="20"&gt;&lt;/maxExclusive&gt;
			&lt;minExclusive value="1"&gt;&lt;/minExclusive&gt;
		&lt;/restriction&gt;
	&lt;/simpleType&gt;
&lt;/element&gt;

•	If we set the value of maxExclusive to “120” for example, it would generate an error since 119 is outside the valid space of “tns:IntegerRestriction100”
Example: Restrictions using Regex
•	We are also able to apply regular expression patterns as a restriction
•	E.g., we can create a pattern so that only a 3 digit number followed by a hyphen is allowed
&lt;element name="StringPattern"&gt;
	&lt;simpleType&gt;
		&lt;restriction base="string"&gt;
			&lt;pattern value="\d{3}-[A-Z]{2}" /&gt;
		&lt;/restriction&gt;
	&lt;/simpleType&gt;
&lt;/element&gt;

Simple Type Summary
Restriction Facets Summary
Facet	Meaning
minExclusive	Value must be greater than x
minInclusive	Value must be greater than or equal to x
maxInclusive	Value must be less than or equal to x
minInclusive	Value must greater than or equal to x
length	The length of the value must be equal to x
minLength	The length must be greater than or equal to x
maxLength	The length must be less than or equal to x
totalDigits	The number of significant digits must be less than or equal to x
fractionDigits	The number of fractional digits must be less than or equal to x
whiteSpace	The schema processor should either preserve, replace or collapse the whitespace
enumeration	x is one of the valid values
pattern 	x is one of the regular expressions that the value may match
explicitTimezone	The time zone of date/time value is required, optional or prohibited
assertion	The value must conform to a constraint in the XPath expression

Example Use Case: Patient Information
•	We need to create a schema file to hold patient information
•	The current fields we need to collect are the patients name, age, gender, email, and phone.
&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;schema xmlns="http://www.w3.org/2001/XMLSchema"
	targetNamespace="http://www.shivkumar.org/Patient"
	xmlns:tns="http://www.shivkumar.org/Patient"
	elementFormDefault="qualified"&gt;

	&lt;!-- * We shall create a schema to create xml files for patients
           * The patients have the following data fields: name, age, email,             
             gender, phone --&gt;
	&lt;complexType name="Patient"&gt;
		&lt;sequence&gt;
			&lt;element name="name"&gt;
				&lt;!-- Using an anonymous simple type: --&gt;
				&lt;simpleType&gt;
					&lt;restriction base="string"&gt;
						&lt;maxLength value="15"&gt;&lt;/maxLength&gt;
					&lt;/restriction&gt;
				&lt;/simpleType&gt;
			&lt;/element&gt;
			&lt;element name="age" type="integer" /&gt;
			&lt;element name="email" type="string" /&gt;
			&lt;element name="gender" type="string"/&gt; 
			&lt;element name="phone" type="string" /&gt;
		&lt;/sequence&gt;
	&lt;/complexType&gt;

&lt;/schema&gt;

Creating Complex Types 
Complex Types Definition
•	We’ve defined a complex as a type which has an attribute and/or child elements. 
•	Complex Types have 4 different content models: simple content (text and attributes), empty (no text but has attributes), element only (no intermingled text), mixed (intermingled text)
•	We can deterministically define what model our complex types will fit into
•	Using model groups like sequence, all, choice lets us define the ordering and occurrence of elements
Choice Model Group
•	The choice model group allows only one element to be defined in the instance.
•	Having 0 or &gt;1 will yield an error
Example
&lt;element name="Patient" type="tns:PatientHealth"&gt;&lt;/element&gt;
	&lt;complexType name="PatientHealth"&gt;
	&lt;choice&gt;
		&lt;element name="weightLbs" type="decimal"/&gt;
		&lt;element name="WeightKg" type="integer"/&gt;
	&lt;/choice&gt;
&lt;/complexType&gt;

&lt;tns:Patient
	xmlns:tns="http://www.example.org/ChoiceGroupExample"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.example.org/ChoiceGroupExample ChoiceGroup.xsd "&gt;
	&lt;tns:WeightKg&gt;12&lt;/tns:WeightKg&gt;
&lt;/tns:Patient&gt;

Sequence Model Group
•	We have already used this model group in our Patient use case example
•	It simply indicates that the elements must appear in the same order as the elements in the sequence group
•	We can use facets like minOccurs and MaxOccurs to make element optional or enable them to appear multiple times
Example
&lt;element name="Patient" type="tns:sequenceGroup"/&gt;	 
&lt;complexType name="sequenceGroup"&gt;
	&lt;sequence&gt;
		&lt;element name="weight" type="integer"/&gt;
		&lt;element name="height" type="integer"/&gt;
		&lt;element name="age" type="integer"/&gt;
		&lt;element name="disease" type="string" minOccurs="0" 
                            maxOccurs="unbounded"/&gt;
	&lt;/sequence&gt;
&lt;/complexType&gt;

  &lt;!--  The following element is optional
  		We can also include multiple diseases but they must appear together
  		I.e. we can not have a disease element at the top --&gt;
  &lt;tns:disease&gt;Cancer&lt;/tns:disease&gt;
  &lt;tns:disease&gt;Diabetes&lt;/tns:disease&gt;
  &lt;tns:disease&gt;Heart Disease&lt;/tns:disease&gt;




