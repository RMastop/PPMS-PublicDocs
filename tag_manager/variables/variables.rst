.. _location: https://developer.mozilla.org/en-US/docs/Web/API/Location
.. _ID: https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id
.. _CSS Selectors: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors
.. _XML Path Language: https://www.w3.org/TR/1999/REC-xpath-19991116/
.. _cookie: https://developer.mozilla.org/en-US/docs/Web/API/Document/cookie
.. _window: https://developer.mozilla.org/en-US/docs/Web/API/Window
.. _document: https://developer.mozilla.org/en-US/docs/Web/API/Document
.. _localStorage: https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage
.. _URI encoded: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURI
.. _decodeURI: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/decodeURI
.. _document.write: https://developer.mozilla.org/en-US/docs/Web/API/Document/write

Variables
=========

Intro
-----
Variable is a placeholder for a value that will be provided when tag is run.
It can be defined in TagManager's **Variables** or via **dataLayer** push in JavaScript.
Tag Manager's variable can be used in tag templates, custom tags and triggers' conditions, but dataLayer's defined variable can only be used in tags.
For it to be usable in conditions it needs to be passed to Tag Manager's dataLayer variable type.

When one want to use a variable it is syntactically a text wrapped in double curly braces, eg. ``{{ myVariable }}``
Our custom tag with variable could look like this:

.. code-block:: html

    <script type="text/javascript">
        console.log('value of my variable: ' + {{ strVariable }});
    </script>

Tag Manager takes measure to properly replace this placeholder with variable value.
That means if value is string it is properly wrapped with string delimiter - apostrophes.

We could also write this snippet following way:

.. code-block:: html

    <script type="text/javascript">
        console.log('value of my variable: {{ strVariable }}');
    </script>

And that would work as well. Tag Manager is knowledgeable enough to not wrap our variable in string delimiters.

And the output would be identical to previous one, in browsers console we would see ``value of my variable: testString`` if we have set **strVariable**'s value to **testString**.

Why would you need variables ?
------------------------------
Simplest explanation is to store api keys in single place and use them in your tags via variables.
More advanced use would be to get even more information to your scripts - you could simply once get a **GET parameter** and reuse it in your tags.
You can also pass some data from your CMS via **dataLayer** variables, for example user identifiers.

Defining a variable in Tag Manager
----------------------------------
When in tag manager go to **Variables** tab and then **+ Create new variable** option on the left pane.
Please see the image for visual guidance:

.. thumbnail:: images/create-variable.png
    :group: creating-variable
    :width: 640px
    :alt: create new variable

Input for variable name will pop up:

.. thumbnail:: images/test-var.png
    :group: creating-variable
    :width: 640px
    :alt: variable name input

You can choose one of the following variable types:

.. thumbnail:: images/variable-types.png
    :group: creating-variable
    :width: 640px
    :alt: variable types

URL
^^^
.. https://www.tablesgenerator.com/text_tables

+---------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Type          | Image                                   | Description                                                                                                                                        |
+===============+=========================================+====================================================================================================================================================+
| GET parameter | .. thumbnail:: images/get-parameter.png | You can pass selected GET parameter to this variable.                                                                                              |
|               |     :group: url-variable                | For example for url ``https://piwik.pro?source=newsletter&medium=email`` you can choose **source** to have **newsletter** passed to your variable. |
|               |     :width: 320px                       |                                                                                                                                                    |
|               |     :alt: GET parameter                 | Value specification:                                                                                                                               |
|               |                                         |                                                                                                                                                    |
|               |                                         | - when your get parameter is not present or has no value, then variable value will be an empty string,                                             |
|               |                                         | - numeric strings will be converted to numbers,                                                                                                    |
|               |                                         | - TRUE, true, FALSE, false string will be converted to boolean values,                                                                             |
+---------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Query         | .. thumbnail:: images/query.png         | With this option our variable will get full query string.                                                                                          |
|               |     :group: url-variable                | For example for url ``https://piwik.pro?source=newsletter&medium=email`` you will get **source=newsletter&medium=email** as your variable's value. |
|               |     :height: 320px                      |                                                                                                                                                    |
|               |     :alt: query                         | Value specification:                                                                                                                               |
|               |                                         |                                                                                                                                                    |
|               |                                         | - when your query string is empty, this value holds empty string                                                                                   |
+---------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
| Protocol      | .. thumbnail:: images/protocol.png      | Here your variable will receive http or https as a value.                                                                                          |
|               |     :group: url-variable                |                                                                                                                                                    |
|               |     :width: 320px                       | Value specification:                                                                                                                               |
|               |     :alt: protocol                      |                                                                                                                                                    |
|               |                                         | - this variable will always hold either http or https                                                                                              |
+---------------+-----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

Random number
^^^^^^^^^^^^^
This variable type provide random value between 0 and 1 (inclusive of 0, but not 1).
Variable has always a value and its type is numerical.

Example values:

- 0.8452040655517055
- 0.6075614549571422
- 0.44718786263204824
- 0.13507537026019567

Document
^^^^^^^^
With **Document** variable type you can access any `document`_ object property.

.. thumbnail:: images/document.png
        :group: document-variable
        :width: 480px
        :alt: protocol

As seen on the screenshot you can assign objects properties after the dot sign.
Of course you could pass also a **location** and in your custom tag you will have an `location`_ object.

Most common properties you would want to use are:

- title
- location

  - protocol
  - host
  - href
  - hash
  - pathname
  - search
- domain
- URL
- documentURI
- referrer

Variable has always value and its type depends on document property assigned.
All mentioned above are of string type.

DOM element
^^^^^^^^^^^
+--------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| Type         | Image                                  | Description                                                                                                                  |
+==============+========================================+==============================================================================================================================+
| Element ID   | .. thumbnail:: images/element-id.png   | You can select HTML element by its `ID`_ attribute.                                                                          |
|              |     :group: dom-element-variable       | Just write it's value into input field.                                                                                      |
|              |     :width: 320px                      |                                                                                                                              |
|              |     :alt: GET parameter                | ID attribute is unique on the page, so only one element will be used to derive the variable value.                           |
+--------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| CSS selector | .. thumbnail:: images/css-selector.png | You can select one or more elements using `CSS selectors`_.                                                                  |
|              |     :group: dom-element-variable       |                                                                                                                              |
|              |     :height: 320px                     | Examples:                                                                                                                    |
|              |     :alt: query                        |                                                                                                                              |
|              |                                        | - div.section - will return all *div* elements that have *section* class (this is hard with **XPath**)                       |
|              |                                        | - a[title] - will return all *a* elements that have *title* attribute                                                        |
+--------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| XPath        | .. thumbnail:: images/xpath.png        | You can select one or more elements using `XML Path Language`_.                                                              |
|              |     :group: dom-element-variable       |                                                                                                                              |
|              |     :width: 320px                      | Examples:                                                                                                                    |
|              |     :alt: protocol                     |                                                                                                                              |
|              |                                        | - //div[contains(@class, 'section')] - will return all *div* elements that have *section* as a substring of class attribute  |
|              |                                        | - //a[@title] - will return all *a* elements that have *title* attribute                                                     |
|              |                                        | - //p[a] - will return all *p* elements with an *a* child (this is impossible to select with **CSS selectors**)              |
+--------------+----------------------------------------+------------------------------------------------------------------------------------------------------------------------------+

Value specification:

- if **Extract text content of an element** is unchecked then variable will hold a value of boolean type, true if element is found, false otherwise.
- if **Extract text content of an element** is checked then variable will hold text extracted from element (and all its descendants) if element is found, empty string otherwise.

Data layer
^^^^^^^^^^
Data layer is a very powerful feature that allows you to pass data from your CMS or other source available via JavaScript on your page to TagManager.
This is the only way to use this data in your triggers' conditions, because only TagManager's variables can be used there.

.. thumbnail:: images/data-layer.png
    :group: data-layer-variable
    :width: 320px
    :alt: data layer

You just have to fill in **data layer** variable name into input and we are done here.
Now to make it work you have to create data layer variable in the code of your page:

.. code-block:: html

    <script type="text/javascript">
        window.dataLayer = window.dataLayer || []; // make sure dataLayer is initialized
        dataLayer.push({test: 'userId'});
    </script>

With this on your page solution is complete and our TagManager's variable will be assigned value ``userId``.

Value specification: one pan push anything to dataLayer, so we can have all data types here, even function.

Cookie
^^^^^^
This variable type allows us to read `cookie`_ values.
You just need to put cookie name into given input.

.. thumbnail:: images/cookie.png
    :group: cookie-variable
    :width: 320px
    :alt: cookie

Value specification: cookies are actually strings, so one would expect a string as a result.
But we recognize string is not always what we expect, so:

- all numeric strings are converted to numbers,
- TRUE, true, FALSE, false string will be converted to boolean values,

If your cookie is more complex than that (e.g. JSON) you have to handle that yourself.

Constant
^^^^^^^^
This is probably the simplest way to create variable. Constant variable gives us possibility to define for example public api keys for your tracking script in a single place.
You have to type it's value into input.

.. thumbnail:: images/constant.png
    :group: constant-variable
    :width: 320px
    :alt: constant

Value specification:

- all numeric strings are converted to numbers,
- TRUE, true, FALSE, false string will be converted to boolean values,

Custom JavaScript
^^^^^^^^^^^^^^^^^
This is most powerful variable type.
To create variable you have to write a javascript function that ends with return statement.
What is returned from this function will be assigned to the variable.

.. thumbnail:: images/custom-js.png
    :group: custom-js-variable
    :width: 320px
    :alt: custom java script

Since this is JavaScript run in the browser you have some predefined objects available:

- `window`_
- `document`_
- `location`_
- `localStorage`_

Value specification: any type you have available in JavaScript.
Additionally same string conversions are made:

- all numeric strings are converted to numbers,
- TRUE, true, FALSE, false string will be converted to boolean values,

.. attention::
    It may be tempting to use variables inside `Custom JavaScript`_ variable type, but its not yet supported.

Please see following examples to understand how powerful Custom JavaScript variable type is.

.. code-block:: js
    :caption: random number between 0 and 10

    function () {
        return Math.floor(Math.random() * Math.floor(10));
    }
Assigned value will be of type ``number``.

.. code-block:: js
    :caption: constant array (10 primes)

    function () {
        return [2, 3, 5, 7, 11, 13, 17, 19, 23, 29];
    }
Assigned value will be of type ``Array``.

.. code-block:: js
    :caption: DOM element

    function () {
        return null !== document.getElementById('main-header');
    }
Assigned value will be of type ``boolean``. True if element with id ``main-header`` exists, false otherwise.

.. code-block:: js
    :caption: URL hash

    function () {
        return location.hash.replace(/^#/, '');
    }
Assigned value will be of type ``string``. For url ``https://example.com/#about`` we will have ``about`` assigned to variable.
If there will not be a hash in url, empty string will be assigned.

More on dataLayer
-----------------
We have mentioned already `Data layer`_, but what it is exactly ?
It is a global JavaScript object that can be used to trigger custom events or define new variables.
Fired events can be part of conditions in tag triggers, variables can be assigned to `Data layer`_ variables or be used in custom tags.

Most common use of data layer (in case of variables) is to pass to Tag Manager data from your CMS.
That would be usually:

- user identifiers,
- page identifiers,
- page language,
- page title,
- product category

You can pass whole objects, for example:

.. code-block:: html

    <script type="text/javascript">
        window.dataLayer = window.dataLayer || []; // make sure dataLayer is initialized
        dataLayer.push({
            user: {
                id: '7aca235d-d33e-4e33-b7d2-7982850f38d3',
                name: 'Julienne',
                surname: 'Doe'
            }
        });
    </script>
    <script type="text/javascript">
        dataLayer.push({
            product: {
                name: 'Some specific product',
                category: 'Promotions'
            }
        });
    </script>


Using variables in Tag Manager
------------------------------
Tag Manager is smart enough to properly handle variables in tags. There are 4 different cases of using variable.

+-------------------------------+----------------------------+
|              HTML             |             JS             |
+=============+=================+===========+================+
| part of URL | not part of url | in string | outside string |
+-------------+-----------------+-----------+----------------+

As long as context are not mixed everything will work properly.

Lets see each case separately:

.. code-block:: html
    :caption: custom tag, HTML context, variable in url

        <img src="//ab-testing/images/banner_{{abVersion}}.png">

.. code-block:: html
    :caption: custom tag, HTML context, variable not in url

        <div class="layout-{{abVersion}}"> ... some content here ... </div>


.. code-block:: html
    :caption: custom tag, JS context, variable in string
    :name: variable in a string

    <script type="text/javascript">
        (function (d) {
            setTimeout(function () {
                var f = d.getElementsByTagName('script')[0], s = d.createElement('script'); s.type = 'text/javascript';
                s.async = true; s.src = '//example.com/{{ customerID }}/{{ siteToken }}.js'; f.parentNode.insertBefore(s, f);
            }, 1);
        })(document);
    </script>

.. code-block:: html
    :caption: custom tag, JS context, variable not in string

        <script type="text/javascript">
            var _paq = _paq || [];
            _paq.push(['setCustomUrl', {{ url }}]);
            _paq.push(['setDocumentTitle', {{ title }}]);
            _paq.push(['trackPageView']);
        </script>

Example of mixed contexts would be when in script dynamically is generated another script with src attribute and injected with `document.write`_.
Lets see the code:

.. code-block:: html
    :caption: custom tag, mixed context example

    <script type="text/javascript">
        document.write(decodeURI("%3Cscript%20src='" +
            (document.location.protocol === 'https:' ?
                'https://example.com/{{ partition }}/path/{{ guid }}.js' :
                'http://example.com/{{ partition }}/path/{{ guid }}.js') + "'%20type='text/javascript'%3E%3C/script%3E"));
    </script>

As you can see both variables (``partition`` and ``guid``) are used in JavaScript code, but in fact they are part of `URL` of `HTML` tag ``<script>``.
Additionally everything is expected to be `URI encoded`_. This will work as long as variables contain only letters and numbers.
If that's not the case tag have to be rewritten so variables can be escaped properly.

For example:

.. code-block:: html
    :caption: custom tag, mixed context example fixed

        <script type="text/javascript">
            var partition = encodeURI(encodeURI('{{ partition }}'));
            var guid = encodeURI(encodeURI('{{ guid }}'));

            document.write(decodeURI("%3Cscript%20src='" +
                (document.location.protocol === 'https:' ?
                    'https://example.com/' + partition + '/path/' + guid + '.js' :
                    'http://example.com/' + partition + '/path/' + guid + '.js') + "'%20type='text/javascript'%3E%3C/script%3E"));
        </script>

What we have done here is we double encoded variables. That is because whole script is passed via `decodeURI`_ function but we need `URI encoded`_ string to pass it safely to scripts url.

.. caution::

    You may wonder why `variable in a string`_ example is not a mixed context. That is because we are in JS context all the time.
    We build script tag only with JavaScript, we do not output ready HTML.


Using in custom tags
^^^^^^^^^^^^^^^^^^^^
Lets see example custom tag:

.. thumbnail:: images/custom-tag.png
    :group: custom-tag
    :width: 320px
    :alt: custom tag




Using in tag templates
^^^^^^^^^^^^^^^^^^^^^^

