# Tags和Attributes

## 支持的元素（Elements）

React试图支持所有HTML和SVG里面常用的元素。JSX中所有小写的tag都会被渲染成带那个tag的元素。SVG元素则必须被一个`<svg>`元素包含才能正常解析。

### 使用`React.DOM`的工厂方法

如果你不是使用JSX，而是使用`React.DOM.*` API来创建元素，你可能会比较受限，因为`React.DOM.*`支持的元素是比较有限的。

- HTML元素

    `React.DOM.*`支持的HTML元素包括：

    ```js
    a abbr address area article aside audio b base bdi bdo big blockquote body br
    button canvas caption cite code col colgroup data datalist dd del details dfn
    dialog div dl dt em embed fieldset figcaption figure footer form h1 h2 h3 h4 h5
    h6 head header hgroup hr html i iframe img input ins kbd keygen label legend li
    link main map mark menu menuitem meta meter nav noscript object ol optgroup
    option output p param picture pre progress q rp rt ruby s samp script section
    select small source span strong style sub summary sup table tbody td textarea
    tfoot th thead time title tr track u ul var video wbr
    ```

- SVG元素

    `React.DOM.*`支持的SVG元素包括：

    ```js
    circle clipPath defs ellipse g image line linearGradient mask path pattern
    polygon polyline radialGradient rect stop svg text tspan
    ```

## 支持的Attributes

React支持所有的`data-*`和`aria-*`属性，也包括下面列表的每一个属性。

注意：为了符合DOM API标准，所有的属性都是驼峰式的，除了`class`和`for`分别对应为`className`和`htmlFor`。

支持的事件可以参阅[React事件系统](/react/event-system.md)

- HTML Attributes

    支持以下标准属性：

    ```js
    accept acceptCharset accessKey action allowFullScreen allowTransparency alt
    async autoComplete autoFocus autoPlay capture cellPadding cellSpacing challenge
    charSet checked cite classID className colSpan cols content contentEditable
    contextMenu controls coords crossOrigin data dateTime default defer dir
    disabled download draggable encType form formAction formEncType formMethod
    formNoValidate formTarget frameBorder headers height hidden high href hrefLang
    htmlFor httpEquiv icon id inputMode integrity is keyParams keyType kind label
    lang list loop low manifest marginHeight marginWidth max maxLength media
    mediaGroup method min minLength multiple muted name noValidate nonce open
    optimum pattern placeholder poster preload profile radioGroup readOnly rel
    required reversed role rowSpan rows sandbox scope scoped scrolling seamless
    selected shape size sizes span spellCheck src srcDoc srcLang srcSet start step
    style summary tabIndex target title type useMap value width wmode wrap
    ```

    支持以下RDFa属性（一些RDFa属性与标准HTML属性重叠了，所以从支持列表中移除了）：

    ```js
    about datatype inlist prefix property resource typeof vocab
    ```

    另外，也支持以下非标准的属性：

    - 给Mobile Safari的`autoCapitalize autoCorrect`
    - Safari里面给`<link rel="mask-icon" />`的`color`属性
    - HTML microdata的`itemProp itemScope itemType itemRef itemID`
    - 老版本IE的`security`
    - IE的`unselectable`
    - WebKit/Blink中`search`类型的input的`results autoSave`属性

    还有两种React特殊的属性：

    - `dangerouslySetInnerHTML`，用以向一个组件直接插入HTML字符串
    - `suppressContentEditableWarning`，用以消除使用`contentEditable`和`children`时候产生的警告。

- SVG Attributes

    ```js
    accentHeight accumulate additive alignmentBaseline allowReorder alphabetic
    amplitude arabicForm ascent attributeName attributeType autoReverse azimuth
    baseFrequency baseProfile baselineShift bbox begin bias by calcMode capHeight
    clip clipPath clipPathUnits clipRule colorInterpolation
    colorInterpolationFilters colorProfile colorRendering contentScriptType
    contentStyleType cursor cx cy d decelerate descent diffuseConstant direction
    display divisor dominantBaseline dur dx dy edgeMode elevation enableBackground
    end exponent externalResourcesRequired fill fillOpacity fillRule filter
    filterRes filterUnits floodColor floodOpacity focusable fontFamily fontSize
    fontSizeAdjust fontStretch fontStyle fontVariant fontWeight format from fx fy
    g1 g2 glyphName glyphOrientationHorizontal glyphOrientationVertical glyphRef
    gradientTransform gradientUnits hanging horizAdvX horizOriginX ideographic
    imageRendering in in2 intercept k k1 k2 k3 k4 kernelMatrix kernelUnitLength
    kerning keyPoints keySplines keyTimes lengthAdjust letterSpacing lightingColor
    limitingConeAngle local markerEnd markerHeight markerMid markerStart
    markerUnits markerWidth mask maskContentUnits maskUnits mathematical mode
    numOctaves offset opacity operator order orient orientation origin overflow
    overlinePosition overlineThickness paintOrder panose1 pathLength
    patternContentUnits patternTransform patternUnits pointerEvents points
    pointsAtX pointsAtY pointsAtZ preserveAlpha preserveAspectRatio primitiveUnits
    r radius refX refY renderingIntent repeatCount repeatDur requiredExtensions
    requiredFeatures restart result rotate rx ry scale seed shapeRendering slope
    spacing specularConstant specularExponent speed spreadMethod startOffset
    stdDeviation stemh stemv stitchTiles stopColor stopOpacity
    strikethroughPosition strikethroughThickness string stroke strokeDasharray
    strokeDashoffset strokeLinecap strokeLinejoin strokeMiterlimit strokeOpacity
    strokeWidth surfaceScale systemLanguage tableValues targetX targetY textAnchor
    textDecoration textLength textRendering to transform u1 u2 underlinePosition
    underlineThickness unicode unicodeBidi unicodeRange unitsPerEm vAlphabetic
    vHanging vIdeographic vMathematical values vectorEffect version vertAdvY
    vertOriginX vertOriginY viewBox viewTarget visibility widths wordSpacing
    writingMode x x1 x2 xChannelSelector xHeight xlinkActuate xlinkArcrole
    xlinkHref xlinkRole xlinkShow xlinkTitle xlinkType xmlBase xmlLang xmlSpace
    y y1 y2 yChannelSelector z zoomAndPan
    ```

