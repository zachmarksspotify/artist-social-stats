<html>
	<head>
		<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.4.2/jquery.min.js"></script>
		<script type="text/javascript">
			var f_page = "wvumountaineers"; // the page name for your fan page, e.g. the 'wvumountaineers' part of http://facebook.com/wvumountaineers
			var t_page = "westvirginiau"; // the account name for your main twitter account
		
			function add_commas(number) {
				if (number.length > 3) {
					var mod = number.length % 3;
					var output = (mod > 0 ? (number.substring(0,mod)) : '');
					for (i=0 ; i < Math.floor(number.length / 3); i++) {
						if ((mod == 0) && (i == 0)) {
							output += number.substring(mod+ 3 * i, mod + 3 * i + 3);
						} else {
							output+= ',' + number.substring(mod + 3 * i, mod + 3 * i + 3);	
						}
					}
					return (output);
				} else {
					return number;
				}
			}
			
			// when document is ready load the counts
			$(document).ready(function(){
			
				// grab from facebook
				$.getJSON('https://graph.facebook.com/'+f_page+'?callback=?', function(data) {
					var fb_count = data['likes'].toString();
					fb_count = add_commas(fb_count);
					$('#fb_count').html(fb_count);
				});
			
				// grab from twitter
				$.getJSON('http://api.twitter.com/1/users/show.json?screen_name='+t_page+'&callback=?', function(data) {
					twit_count = data['followers_count'].toString();
					twit_count = add_commas(twit_count);
					$('#twitter_count').html(twit_count);
				});
			
			});
		</script>
	</head>
	<body>
		<noscript>The following counts are dynamically populated by JavaScript. You can also directly visit the sources to find the counts at http://facebook.com/[pagename] and http://twitter.com/[accountname]</noscript>

		Facebook fan count: <span id="fb_count"></span><br />
		Twitter follower count: <span id="twitter_count"></span><br />
		<br />
		<em>You could put these spans in nice little badges or something...</em>
	</body>
</html>
