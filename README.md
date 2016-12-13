# file-base64-angularjs
file to base64 using angularjs

On file change, file will be converted to base64 String formate by the angularjs directive. 
And will be appened to the object of a controller. And will call the callback function from the directive.

<h1>Usage</h1>

<h2>HTML</h2>
<pre>
  <code>
  &lt;input type="file" data-ng-base64 data-uploader="uploader()" filez="filez" &gt;
  </code>
</pre>
<p>
<i>data-ng-base64:</i> it is a directive.<br>
<i>data-uploader="uploader()":</i> data-uploader is a callback method passed to directive. uploader() is a function inside controller<br>
<i>filez="filez":</i> filez is a object of a controller which is passed to directive to update base64 string to this object.<br>
</p>

<h2>Angularjs</h2>
<h3>Directive</h3>
<pre>
  <code>
    /*
		 *	This function convert file into base64 format, attach base64 string to 
		 *	scope.accessor.img and calls uploader() function in the controller
		 *	&uploader: call back function
		 */
		app.directive('ngBase64', [function () {
			return {
				restrict: 'A',
				scope: {
					filez: '=',
					callback: '&uploader'
				},
				link: function (scope, iElement, iAttrs) {
					iElement.bind('change', function(event) {
						var reader = new FileReader();
						var files = event.target.files;
						reader.readAsDataURL(files[0]);
						reader.onload = function(loadevent) {
							var fileInfo = files[0];
							scope.$apply(function() {
								scope.filez.basestring = loadevent.target.result;
								scope.callback();
							})
						}
					})
				}
			};
		}])
  </code>
</pre>
