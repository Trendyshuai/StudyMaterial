<h1><center>JsRender</center></h1>

## Playing with JsRender

* ### JsRender templates

    <font color="00ffbb">Template :</font>

    ` <label> Name: </label> {{:name}} `

    <font color="00ffbb">Code:</font>
    ``` Javascript
    var person = {
        name: "Shine Lee"
    };

    var html = myTemplate.render(person);
    ```

    <font color="00ffbb">Full Code :</font>
    ``` html
    <!DOCTYPE html>
    <html>
    <head>
        <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
        <script src="https://www.jsviews.com/download/jsviews.min.js"></script>
        <link href="https://www.jsviews.com/samples/samples.css" rel="stylesheet" />
    </head>
    <body>

        <div id="result"></div>

        <script id="theTmpl" type="text/x-jsrender">
            <!-- HTML Template write in script label. -->
            <label>Name:</label> {{:name}}<br/>
            <label>Age:</label> {{:age}}
        </script>

        <script>
            // Json Data.
            var data = {
            "name": "Adriana",
            "age": 34
            };

            var template = $.templates("#theTmpl");
            // Show result in div.
            template.link("#result", data);
        </script>

    </body>
    </html>
    ```

    ` Array need to change the json data. `

    <font color="00ffbb">Like this :</font>

    ``` Javascript
    // id selector.
    var myTemplate = $.templates("#personTmpl");

    var people = [
    {
        name: "Adriana",
        age: 45
    },
    {
        name: "Robert",
        age: 98
    }
    ];

    var html = myTemplate.render(people);

    $("#peopleList").html(html);
    ```

* ### Else templates

    <font color="ooffbb">{{ for }} & {{ if }} :</font>

    * HTML Code :
    ``` html
    <table><tbody id="peopleList"></tbody></table>

    <script id="peopleTmpl" type="text/x-jsrender">
        <tr><td>
            <ul>
                {{for people}}
                    <li>
                        {{:name}}
                        {{if nickname}}
                            ( {{:nickname}} )
                        {{/if}}
                    </li>
                {{/for}}
            </ul>
        </td></tr>
    </script>
    ```

    * Javascript Code :
    ``` js
    var myTemplate = $.templates("#peopleTmpl");

    var people = [
        {
        name: "Adriana"
        },
        {
        name: "Robert",
        nickname: "Bob"
        }
    ];

    app = {
        people: people
    };

    var html = myTemplate.render(app);

    $("#peopleList").html(html);
    ```

    * effect :
    ```
    · Adriana
    · Robert ( Bob )
    ```

## Quick Start

* ### Define a template
  * Form a string :
    ``` js
    var tmpl = $.templates("Name: {{:name}}");
    ```

  * From a template declared as markup in a script block :
    ``` html
    <script id="myTemplate" type="text/x-jsrender">
        Name: {{:name}}
    </script>

    <script>
        var tmpl = $.templates("#myTemplate");
    </script>
    ```
* ### Render a template
    ``` js
    var tmpl = $.templates(" Name: {{:name}}<br/> ");
    var person = {name: "Jim"};

    // Render template for person object
    var html = tmpl.render(person); // ready for insertion, e.g $("#container").html(html);

    // result: "Name: Jim<br/> "
    var people = [{name: "Jim"}, {name: "Pedro"}];

    // Render template for people array
    var html = tmpl.render(people); // ready for insertion...

    // result: "Name: Jim<br/> Name: Pedro<br/> "
    ```
* ### Register a named template – and render it
    ``` js
    // Register named template "myTmpl1", from string 
    $.templates("myTmpl1", "Name: {{:name}}<br/> ");
    // (or from script block: $.templates("myTmpl1", "#myTemplate"); ...)

    var person = {name: "Jim"};

    // Render named template
    var html = $.render.myTmpl1(person);

    // result: "Name: Jim<br/> "
    ```


<h1><center>JsRender API</center></h1>

## Tag syntax
Template tags in JsRender use the Mustache style: ` {{...}} `.<br>
(You can choose different delimiters, such as ` <%...%> `, using ` $.views.settings.delimiters("<%", "%>") `.

* Tags without content

    The most common JsRender tags are ` {{: pathOrExpr}} ` – which inserts the value of the path or expression, and ` {{> pathOrExpr}} ` - which inserts the HTML-encoded value of the path or expression.

* Block tags – tags with content:

    <b>All other built-in tags, as well as all custom tags, use the block tag syntax:</b>
    ||||
    |---|---|---|
    |{{include ...}}...{{/include}}|or|{{include .../}}|
    |{{for}}...{{/for}}|or|   {{for.../}}|
    |{{props}}...{{/props}}|or|   {{props .../}}|
    |{{if}}...{{/if}}|or|   {{if .../}}|
    |{{myCustomTag}}...{{/myCustomTag}}|or|{{myCustomTag .../}}|

## Paths and expressions





<h1><center>JsRender Cont..</center></h1>
Some of the basic syntaxes followed in JsRender:

* ` <script id="element" type="text/x-jsrender"></script> `
* {{ }} : JsRender Tag
* {{:Data}} or {{>Data}} : 2 Different ways to access
* data
* {{for}} ... {{/for}} : for Loop
* {{if condition...}} ... {{/if}} : if-Else Conditions
* {{:~functionName(param1, param2, ...)}} : Helper Functions.
* And Many more...

Example:
HTML Code:
``` html
<script id="template" type="text/x-jsrender">
    {{for #data}}
        {{if ID > 3}}
            <li>{{>ID}} <t><t> {{>Name}} <t><t> {{>MobileNo}}</li>
        {{/if}}
    {{/for}}
</script>
```

Js Code:
``` html
<script type = "text/javascript">
    $.ajax({
        url: 'getData.ashx',
        dataType: 'json',
        success: processData,
        error : handleError
    });

    function processData(data, status){
        $('#elem').html($('#template').render(data));
    }
    function handleError(msg, data){
        alert(msg);
    }
</script>
```
