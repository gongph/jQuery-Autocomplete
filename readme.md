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
| `onSearchError` | `function (query, jqXHR, textStatus, errorThrown) {}` called if Ajax request fails. `this` is bound to input element 当异步查询错误时调用。 `this` 绑定的是 输入框元素|
| `onHide` | `function (container) {}` called before container will be hidden 当查询结果容器隐藏时调用|


### Local only settings
### 仅限本地设置
| Setting | Default | Description |
| :--- | :--- | :--- |
| `lookupLimit` | `no limit` | Number of maximum results to display for local lookup 显示本地查找的最大结果数|
| `lookup` | n/a | Callback function or lookup array for the suggestions. It may be array of strings or `suggestion` object literals 一个回调函数或者结果及数组。它可以是一个字符串数组或 `suggestion` 对象字面量|
| `suggestion` | n/a | Not a settings, but in the context of above row, a suggestion is an object literal with the following format: `{ value: 'string', data: any }` 非设置选项，但是上一行的内容里，每个 suggestion 都是一个包含 `{value: 'string', data: any }` 的对象字面量|
| `lookupFilter` | n/a | `function (suggestion, query, queryLowerCase) {}` filter function for local lookups. By default it does partial string match (case insensitive) 用于本地查找的过滤函数。默认情况下它会进行部分字符串匹配（不区分大小写）|

### Ajax only settings
### 仅限 Ajax 设置
| Setting | Default | Description |
| :--- | :--- | :--- |
| `serviceUrl` | n/a | Server side URL or callback function that returns serviceUrl string 服务器端URL或回调函数，返回 serviceUrl 字符串|
| `type` | `GET` | Ajax request type to get suggestions Ajax 请求类型|
| `dataType` | `text` | type of data returned from server. Either `text`, `json`  or `jsonp`, which will cause the autocomplete to use jsonp. You may return a json object in your callback when using jsonp 从服务器返回的数据类型。无论使用 `text`, `json`, 还是 `jsonp` 中的哪一个都将自动转成 jsonp。当使用 jsonp 的时候你可以在你的回调函数中返回一个 json 对象|
| `paramName` | `query` | The name of the request parameter that contains the query 自定义查询名字|
| `params` | optional | Additional parameters to pass with the request 请求传递的其他参数|
| `deferRequestBy` | `0` | Number of miliseconds to defer Ajax request 推迟Ajax请求的毫秒数|
| `ajaxSettings` | optional | Any additional [Ajax Settings](http://api.jquery.com/jquery.ajax/#jQuery-ajax-settings) that configure the jQuery Ajax request 任意 jQuery Ajax 请求配置|

## Default Options
## 默认选项

Default options for all instances can be accessed via `$.Autocomplete.defaults`.
所有实例的默认选项都可以通过 `$ .Autocomplete.defaults` 访问。

## Instance Methods
## 实例方法

Autocomplete instance has following methods:
自动完成实例有如下方法：

* `setOptions(options)`: you may update any option at any time. Options are listed above. 您可以随时更新任何选项。参考上面的选项。
* `clear`: clears suggestion cache and current suggestions. 清除缓存结果和当前的查询结果。
* `clearCache`: clears suggestion cache. 清除缓存。
* `disable`: deactivate autocomplete. 停用自动完成
* `enable`: activates autocomplete if it was deactivated before. 如果当前自动完成为停用状态则激活。
* `hide`: hides suggestions. 隐藏查询结果
* `dispose`: destroys autocomplete instance. All events are detached and suggestion containers removed. 销毁自动完成实例。所有的事件被解除，查询结果容器被删除。

There are two ways that you can invoke Autocomplete method. One is calling autocomplete on jQuery object and passing method name as string literal.
有两种方法可以调用自动完成方法。一个是在jQuery对象上调用自动完成，并将方法名称作为字符串文字传递。

If method has arguments, arguments are passed as consecutive parameters:
如果方法有参数，则参数作为连续参数传递：

```javascript
$('#autocomplete').autocomplete('disable');
$('#autocomplete').autocomplete('setOptions', options);
```

Or you can get Autocomplete instance by calling autcomplete on jQuery object without any parameters and then invoke desired method.
或者，您可以通过调用 jQuery 对象上的 autcomplete 方法而不用任何参数来获得 Autocomplete 实例，然后调用所需的方法。

```javascript
$('#autocomplete').autocomplete().disable();
$('#autocomplete').autocomplete().setOptions(options);
```

## Usage(用法)

Html:

```html
<input type="text" name="country" id="autocomplete"/>
```

Ajax lookup(Ajax查询):

```javascript
$('#autocomplete').autocomplete({
    serviceUrl: '/autocomplete/countries',
    onSelect: function (suggestion) {
        alert('You selected: ' + suggestion.value + ', ' + suggestion.data);
    }
});
```

Local lookup (no Ajax):
本地查询（非Ajax）

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
自定义查询方法：
```javascript

$('#autocomplete').autocomplete({
    lookup: function (query, done) {
        // Do Ajax call or lookup locally, when done,
        // call the callback and pass your results:
        // Ajax 或本地查询，完成后，
        // 调用回调函数并传递你的查询结果：
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

## Styling（样式）

Generated HTML markup for suggestions is displayed below. You may style it any way you'd like.
查询结果生成的 HTML 标记元素如下所示，你可以按照自己的喜好自定义样式。

```html
<div class="autocomplete-suggestions">
    <div class="autocomplete-group"><strong>NHL</strong></div>
    <div class="autocomplete-suggestion autocomplete-selected">...</div>
    <div class="autocomplete-suggestion">...</div>
    <div class="autocomplete-suggestion">...</div>
</div>
```

Style sample（示例样式）:

```css
.autocomplete-suggestions { border: 1px solid #999; background: #FFF; overflow: auto; }
.autocomplete-suggestion { padding: 2px 5px; white-space: nowrap; overflow: hidden; }
.autocomplete-selected { background: #F0F0F0; }
.autocomplete-suggestions strong { font-weight: normal; color: #3399FF; }
.autocomplete-group { padding: 2px 5px; }
.autocomplete-group strong { display: block; border-bottom: 1px solid #000; }
```


## Response Format
## 响应数据格式

Response from the server must be JSON formatted following JavaScript object:
来自服务器的响应数据必须是符合下面 JavaScript 对象的 JSON 格式：

```javascript
{
    // Query is not required as of version 1.2.5
    // Query 从 1.2.5 版本以后不是必须的
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
Data 可以是任意类型的值或对象。数据对象被传递给 formatResults 函数和 onSelect 回调。另外，如果没有 data 属性，你只需给 suggestions 传一个字符串数组即可，就像下面这样：

```json
{
    "query": "Unit",
    "suggestions": ["United Arab Emirates", "United Kingdom", "United States"]
}
```

## Non standard query/results
## 非标准查询/结果

If your Ajax service expects the query in a different format, and returns data in a different format than the standard response,
you can supply the "paramName" and "transformResult" options:
如果您的 Ajax 服务需要使用其他格式的查询，并以不同于标准响应的格式返回数据，你可以提供 “paramName” 和 “transformResult” 选项：

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
## 分组结果

Specify `groupBy` option of you data property if you wish results to be displayed in groups. For example, set `groupBy: 'category'` if your suggestion data format is:
如果你希望把查询结果按组显示，请在 `groupBy` 中指定你的 data 属性。例如，如果你的查询结果的数据格式是下面这样子，设置 `groupBy: 'category'` 将会按 category 分组显示：

```javascript
[
    { value: 'Chicago Blackhawks', data: { category: 'NHL' } },
    { value: 'Chicago Bulls', data: { category: 'NBA' } }
]
```

Results will be formatted into two groups **NHL** and **NBA**.
结果将被格式化为两组 **NHL** 和 **NBA** 。

## Known Issues
## 已知问题

If you use it with jQuery UI library it also has plugin named `autocomplete`. In this case you can use plugin alias `devbridgeAutocomplete`:
如果你使用jQuery UI库，它也有一个名为`autocomplete`的插件。在这种情况下，你可以使用插件别名 `devbridgeAutocomplete` ：

```javascript
$('.autocomplete').devbridgeAutocomplete({ ... });
```

It seems that for mobile Safari click events are only triggered if the CSS of the object being tapped has the cursor set to pointer:
似乎只有当被点击的对象的 CSS 将光标设置为指针时，才会触发移动 Safari 单击事件：

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
