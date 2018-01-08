Devbridge Group accelerates software to market for enterprise clients through dedicated product teams, user experience and software engineering expertise.

[www.devbridge.com](http://www.devbridge.com/)

# Ajax Autocomplete for jQuery
# 用于 jQuery 的 Ajax 自动完成插件

Ajax Autocomplete for jQuery allows you to easily create
autocomplete/autosuggest boxes for text input fields.
用于 jQuery 的 Ajax 自动完成插件使你能够轻松创建一个文本输入字段的自动完成/自动提示框。

It has no dependencies other than jQuery.
除了 jQuery ，没有任何依赖。

The standard jquery.autocomplete.js file is around 13KB when minified.
压缩后， jquery.autocomplete.js 文件大约只有 13KB。

## API
The following sets up autocomplete for input fields where `options` is an object literal that defines the settings to use for the autocomplete plugin.  All available option settings are shown in the tables below.  
下列选项是用来定义自动完成插件的一些选项， `options` 是一个对象字面量，其所有可用的选项如下：

```js
$(selector).autocomplete(options);
```
### General settings (local and Ajax) 
### 通用设置（本地 和 Ajax）
| Setting | Default | Description |
| :--- | :--- | :--- |
| `noCache` | `false` | Boolean value indicating whether to cache suggestion results 布尔值，是否缓存查询结果|
| `delimiter` | optional | String or RegExp, that splits input value and takes last part to as query for suggestions. Useful when for example you need to fill list of  comma separated values. 字符串或正则表达式，用来分割多个文本查询内容。当你需要用逗号分割查询值时，这个选项很有用|
| `minChars` | `1` | Minimum number of characters required to trigger autosuggest 触发自动提示所需的最少字符数|
| `triggerSelectOnValidInput` | `true` | Boolean value indicating if `select` should be triggered if it matches suggestion 如果查询匹配结果，则触发选择|
| `preventBadQueries` | `true` | Boolean value indicating if it should prevent future Ajax requests for queries with the same root if no results were returned. E.g. if `Jam` returns no suggestions, it will not fire for any future query that starts with `Jam` 布尔值，指示在没有返回结果的情况下是否应该阻止未来使用相同根的查询的Ajax请求。例如。如果 `Jam` 没有返回任何建议，它将不会触发任何以 `Jam` 开始的查询|
| `autoSelectFirst` | `false` | If set to `true`, first item will be selected when showing suggestions 第一个查询结果将被设置选中状态|
| `beforeRender` | optional | `function (container, suggestions) {}` called before displaying the suggestions. You may manipulate suggestions DOM before it is displayed 显示查询结果之前调用，在这之前你可以操作查询结果 DOM |
| `formatResult` | optional | `function (suggestion, currentValue) {}` custom function to format suggestion entry inside suggestions container 自定义格式化查询结果容器|
| `formatGroup` | optional | `function (suggestion, category) {}` custom function to format group header 自定义分组头|
| `groupBy` | optional | property name of the suggestion `data` object, by which results should be grouped 指定查询结果 `data` 对象中的哪个属性可以作为分组属性|
| `maxHeight` | `300` | Maximum height of the suggestions container in pixels 设置查询结果容器的最大高度（以像素为单位）|
| `width` | `auto` | Suggestions container width in pixels, e.g.: 300, `flex` for max suggestion size and `auto` takes input field width 设置查询结果容器的宽度（以像素为单位），例如：300，`flex` 取最宽的条目宽度，`auto` 采用文本框的宽度|
| `zIndex` | `9999` | 'z-index' for suggestions container 设置查询结果容器的 z 轴索引|
| `appendTo` | optional | Container where suggestions will be appended. Default value `document.body`. Can be jQuery object, selector or HTML element. Make sure to set `position: absolute` or `position: relative` for that element 查询结果容器将被添加到哪里。默认是 `document.body`。可以是 jQuery 对象，选择器或这 HTML 元素。确保为该元素设置 `position: absolute` 或者 `position: relative`|
| `forceFixPosition` | `false` | Suggestions are automatically positioned when their container is appended to body (look at `appendTo` option), in other cases suggestions are rendered but no positioning is applied. Set this option to force auto positioning in other cases 当他们的容器添加到 body 上时，查询结果容器将会自动定位（查看 `appendTo` 选项），除此之外，容器渲染后则不会自动定位。设置此选项可以解决这个问题|
| `orientation` | `bottom` | Vertical orientation of the displayed suggestions, available values are `auto`, `top`, `bottom`.  If set to `auto`, the suggestions will be orientated it the way that place them closer to middle of the view port 设置查询结果容器在垂直方向上的位置，可选值有 `auto`, `top`, `bottom`。如果设置成 `auto`，容器将被定位到靠近视口中间的位置|
| `preserveInput` | `false` | If `true`, input value stays the same when navigating over suggestions 如果为 `true`，始终保持文本框中的查询内容不变|
| `showNoSuggestionNotice` | `false` | When no matching results, display a notification label 当没有匹配到查询结果时，显示一个通知文本内容|
| `noSuggestionNotice` | `No results` | Text or htmlString or Element or jQuery object for no matching results label 文本或 html 字符串或 元素 或 jQuery 对象，用来自定义无匹配通知文本内容|
| `onInvalidateSelection` | optional | `function () {}` called when input is altered after selection has been made. `this` is bound to input element 选择完成，改变输入内容时调用|
| `tabDisabled` | `false` | Set to true to leave the cursor in the input field after the user tabs to select a suggestion 设置为 true 时，当用户选择一个结果后，鼠标停留在文本输入框中|


### Event function settings (local and Ajax) 
### 事件（本地和 Ajax）
| Event setting | Function description |
| :--- | :--- |
| `onSearchStart` | `function (params) {}` called before Ajax request. `this` is bound to input element Ajax请求之前调用。 `this` 绑定的是输入框元素|
| `onHint` | `function (container) {}` used to change input value to first suggestion automatically 自动将输入值更改为第一个建议|
| `onSearchComplete` | `function (query, suggestions) {}` called after Ajax response is processed. `this` is bound to input element. `suggestions` is an array containing the results 在处理完Ajax响应后调用。`this` 绑定的是输入框元素，`suggestions` 是一个查询结果数组|
| `transformResult` | `function(response, originalQuery) {}` called after the result of the query is ready. Converts the result into response.suggestions format 查询结果准备就绪后调用。将结果转换为 response.suggestions 格式|
| `onSelect` | `function (suggestion) {}` Callback function invoked when user selects suggestion from the list. `this` inside callback refers to input HtmlElement. 当用户选择一个查询结果条目时调用。回调中的 `this` 引用的是 输入框元素对象|
| `onSearchError` | `function (query, jqXHR, textStatus, errorThrown) {}` called if Ajax request fails. `this` is bound to input element 当异步查询错误是调用。 `this` 绑定的是 输入框元素|
| `onHide` | `function (container) {}` called before container will be hidden 当查询结果容器隐藏时调用|


### Local only settings
| Setting | Default | Description |
| :--- | :--- | :--- |
| `lookupLimit` | `no limit` | Number of maximum results to display for local lookup |
| `lookup` | n/a | Callback function or lookup array for the suggestions. It may be array of strings or `suggestion` object literals |
| `suggestion` | n/a | Not a settings, but in the context of above row, a suggestion is an object literal with the following format: `{ value: 'string', data: any }` |
| `lookupFilter` | n/a | `function (suggestion, query, queryLowerCase) {}` filter function for local lookups. By default it does partial string match (case insensitive) |

### Ajax only settings
| Setting | Default | Description |
| :--- | :--- | :--- |
| `serviceUrl` | n/a | Server side URL or callback function that returns serviceUrl string |
| `type` | `GET` | Ajax request type to get suggestions |
| `dataType` | `text` | type of data returned from server. Either `text`, `json`  or `jsonp`, which will cause the autocomplete to use jsonp. You may return a json object in your callback when using jsonp |
| `paramName` | `query` | The name of the request parameter that contains the query |
| `params` | optional | Additional parameters to pass with the request |
| `deferRequestBy` | `0` | Number of miliseconds to defer Ajax request |
| `ajaxSettings` | optional | Any additional [Ajax Settings](http://api.jquery.com/jquery.ajax/#jQuery-ajax-settings) that configure the jQuery Ajax request |

## Default Options

Default options for all instances can be accessed via `$.Autocomplete.defaults`.

## Instance Methods

Autocomplete instance has following methods:

* `setOptions(options)`: you may update any option at any time. Options are listed above.
* `clear`: clears suggestion cache and current suggestions.
* `clearCache`: clears suggestion cache.
* `disable`: deactivate autocomplete.
* `enable`: activates autocomplete if it was deactivated before.
* `hide`: hides suggestions.
* `dispose`: destroys autocomplete instance. All events are detached and suggestion containers removed.

There are two ways that you can invoke Autocomplete method. One is calling autocomplete on jQuery object and passing method name as string literal.
If method has arguments, arguments are passed as consecutive parameters:

```javascript
$('#autocomplete').autocomplete('disable');
$('#autocomplete').autocomplete('setOptions', options);
```

Or you can get Autocomplete instance by calling autcomplete on jQuery object without any parameters and then invoke desired method.

```javascript
$('#autocomplete').autocomplete().disable();
$('#autocomplete').autocomplete().setOptions(options);
```

## Usage

Html:

```html
<input type="text" name="country" id="autocomplete"/>
```

Ajax lookup:

```javascript
$('#autocomplete').autocomplete({
    serviceUrl: '/autocomplete/countries',
    onSelect: function (suggestion) {
        alert('You selected: ' + suggestion.value + ', ' + suggestion.data);
    }
});
```

Local lookup (no Ajax):

```javascript
var countries = [
    { value: 'Andorra', data: 'AD' },
    // ...
    { value: 'Zimbabwe', data: 'ZZ' }
];

$('#autocomplete').autocomplete({
    lookup: countries,
    onSelect: function (suggestion) {
        alert('You selected: ' + suggestion.value + ', ' + suggestion.data);
    }
});
```

Custom lookup function:
```javascript

$('#autocomplete').autocomplete({
    lookup: function (query, done) {
        // Do Ajax call or lookup locally, when done,
        // call the callback and pass your results:
        var result = {
            suggestions: [
                { "value": "United Arab Emirates", "data": "AE" },
                { "value": "United Kingdom",       "data": "UK" },
                { "value": "United States",        "data": "US" }
            ]
        };

        done(result);
    },
    onSelect: function (suggestion) {
        alert('You selected: ' + suggestion.value + ', ' + suggestion.data);
    }
});
```

## Styling

Generated HTML markup for suggestions is displayed below. You may style it any way you'd like.

```html
<div class="autocomplete-suggestions">
    <div class="autocomplete-group"><strong>NHL</strong></div>
    <div class="autocomplete-suggestion autocomplete-selected">...</div>
    <div class="autocomplete-suggestion">...</div>
    <div class="autocomplete-suggestion">...</div>
</div>
```

Style sample:

```css
.autocomplete-suggestions { border: 1px solid #999; background: #FFF; overflow: auto; }
.autocomplete-suggestion { padding: 2px 5px; white-space: nowrap; overflow: hidden; }
.autocomplete-selected { background: #F0F0F0; }
.autocomplete-suggestions strong { font-weight: normal; color: #3399FF; }
.autocomplete-group { padding: 2px 5px; }
.autocomplete-group strong { display: block; border-bottom: 1px solid #000; }
```


## Response Format

Response from the server must be JSON formatted following JavaScript object:

```javascript
{
    // Query is not required as of version 1.2.5
    "query": "Unit",
    "suggestions": [
        { "value": "United Arab Emirates", "data": "AE" },
        { "value": "United Kingdom",       "data": "UK" },
        { "value": "United States",        "data": "US" }
    ]
}
```

Data can be any value or object. Data object is passed to formatResults function
and onSelect callback. Alternatively, if there is no data you can
supply just a string array for suggestions:

```json
{
    "query": "Unit",
    "suggestions": ["United Arab Emirates", "United Kingdom", "United States"]
}
```

## Non standard query/results

If your Ajax service expects the query in a different format, and returns data in a different format than the standard response,
you can supply the "paramName" and "transformResult" options:

```javascript
$('#autocomplete').autocomplete({
    paramName: 'searchString',
    transformResult: function(response) {
        return {
            suggestions: $.map(response.myData, function(dataItem) {
                return { value: dataItem.valueField, data: dataItem.dataField };
            })
        };
    }
})
```

## Grouping Results

Specify `groupBy` option of you data property if you wish results to be displayed in groups. For example, set `groupBy: 'category'` if your suggestion data format is:

```javascript
[
    { value: 'Chicago Blackhawks', data: { category: 'NHL' } },
    { value: 'Chicago Bulls', data: { category: 'NBA' } }
]
```

Results will be formatted into two groups **NHL** and **NBA**.

## Known Issues

If you use it with jQuery UI library it also has plugin named `autocomplete`. In this case you can use plugin alias `devbridgeAutocomplete`:

```javascript
$('.autocomplete').devbridgeAutocomplete({ ... });
```

It seems that for mobile Safari click events are only triggered if the CSS of the object being tapped has the cursor set to pointer:

    .autocomplete-suggestion { 
        cursor: pointer;
    }

See issue #542

## License

Ajax Autocomplete for jQuery is freely distributable under the
terms of an MIT-style [license](https://github.com/devbridge/jQuery-Autocomplete/blob/master/dist/license.txt).

Copyright notice and permission notice shall be included in all
copies or substantial portions of the Software.

## Authors

Tomas Kirda / [@tkirda](https://twitter.com/tkirda)
