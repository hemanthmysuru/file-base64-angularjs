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
<code>data-ng-base64:</code> it is a directive.<br>
<code>data-uploader="uploader()":</code> data-uploader is a callback method passed to directive. uploader() is a function inside controller<br>
<code>filez="filez":</code> filez is a object of a controller which is passed to directive to update base64 string to this object.<br>
</p>

<h2>Angularjs</h2>
<h3>Controller</h3>
<p>
uploader function is called from the directive synchronusly. Because it is a callback function which is sent from the html input tag
as an attribute <code>data-uploader="uploader()"</code>. And updates the <code>$scope.filez</code> object from the directive itself. Because even it is passed from html input tag as an attribute <code>filez="filez"</code>.
</p>

<pre>
  <code>
  	app.controller('fileCtrl', function($scope) {
		$scope.filez = {};
		$scope.uploader = function() {
			console.log($scope.filez);
		}
	})
  </code>
</pre>


<h3>Directive</h3>
<p>
This directive is invoked by the <code>data-ng-base64</code> attribute inside input tag. This directive will reads the file and convert 
that to base64 formate and append the to <code>scope.filez.basestring</code> like <code>scope.filez.basestring = loadevent.target.result</code>. Finally it calls the callback function <code>uploader()</code> passed to scope <code>callback: '&uploader'</code>, calling inside link <code>scope.callback()</code>
</p>
<pre>
  <code>
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
