# file-base64-angularjs
file to base64 using angularjs

On file change, file will be converted to base64 String formate by the angularjs directive. 
And will be appened to the object of a controller. And will call the callback function from the directive.

# Usage
<strong>html</strong>
  <ul>
      <li>data-ng-base64: it is a directive.</li>
      <li>data-uploader="uploader()": data-uploader is a callback method passed to directive. uploader() is a function inside controller</li>
      <li>filez="filez": filez is a object of a controller which is passed to directive to update base64 string to this object.</li>
  </ul>

<blockquote>
&lt;input type="file" name="" value="" placeholder="" data-ng-base64 data-uploader="uploader()" filez="filez" &gt;
</blockquote>


<strong>angularjs</strong>
