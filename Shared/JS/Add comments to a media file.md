# How to add comments to a media file
- Note that it is only needed for TDSMEDIA files.
- All TDSSLIDE and TDSARTL files have automatic comments integration so no need for sample codes. Everytime you create slides and articles, the comments tool will be added automatically.
- Basically, if you have a custom webpage, you can add the following codes to your HTML code which is stored in a TDSMEDIA file.
- It is simple to link an ULAPPH Cloud Desktop file so it will have a comments capability as long as it is TDSMEDIA, TDSSLIDE or TDSARTL format.
- Before a user can comment, it will first go through reCaptcha verification:

[http://www.ulapph.com/captcha?CC_FUNC=DISP&R=COMMENT&SID=TDSMEDIA-3&TITLE=ULAPPH Portal Website](http://www.ulapph.com/captcha?CC_FUNC=DISP&R=COMMENT&SID=TDSMEDIA-3&TITLE=ULAPPH%20Portal%20Website)


## Header codes to be placed inside the <head> section

    <!-- Comment button -->
    <link rel="stylesheet" href="/lib/css/buttons/buttons.css">

## Main Body codes to be added anywhere in the body

	<!-- Comments & Discussions -->
	<div class="row">
		<div class="col-lg-12">
			<h4 class="heading">Discussions & Comments</h4>
			<div class="row">
            <a href="/captcha?CC_FUNC=DISP&R=COMMENT&SID=TDSMEDIA-3&TITLE=ULAPPH Portal Website" target="TDSMEDIA-3-comments" class="button button-block button-rounded button-primary button-large">View Comments (<span id="comments-count">1</span>)</a>
			</div>
		</div>
	</div>
    
## Footer codes to be added right before the </body> tag

    <!-- Get the current comments count of this page -->
    <script>
        var sid = "TDSMEDIA-3";
        var apiKey = "YOUR-ULAPPH-API-KEY";
        var data = JSON.stringify({"SID":sid});
    	var apicall = httpGetAsync("/media?FUNC_CODE=GET_COMMENTS_COUNT&SID=" + sid + "&API_KEY=" + apiKey, data, apiKey);
    	console.log("apicall: "+apicall);
                	
        function httpGetAsync(theUrl, data, API_KEY)
        { 
            if (window.XMLHttpRequest)
        	  {// code for IE7+, Firefox, Chrome, Opera, Safari
        	  var cxhr2=new XMLHttpRequest();
        	  }
        	else
        	  {// code for IE6, IE5
        	  var cxhr2=new ActiveXObject('MSXML2.XMLHTTP.3.0');
        	  }
            	  
        	cxhr2.open("POST", theUrl, true); 
        	cxhr2.setRequestHeader("Authorization", API_KEY);
        	cxhr2.setRequestHeader("Content-type", "application/json");
        	console.log("sending data: "+data);
        	 cxhr2.onreadystatechange=function()
        	  {
        	  if (cxhr2.readyState==4 && cxhr2.status==200)
        		{
        		var currVal = cxhr2.responseText;
        			if (currVal != "" ) {
        			    console.log("resp: "+currVal);
        			    document.getElementById("comments-count").innerHTML = currVal;
        			}
        		}
        	  }
        	cxhr2.send(data);
        };
    </script>  
    <!-- End comments script-->

