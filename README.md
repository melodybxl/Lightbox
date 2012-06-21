Lightbox
========

------------------- JS ------------------------



var data , data_type, data_size,  data_refresh;
		
jQuery(document).ready(function($) {
 
    $('.lightbox_trigger').click(function(e) {
 
        e.preventDefault();
 
 
         data = $(this).attr("href");
		 data_type = $(this).attr("data-type");
		 data_size = $(this).attr("data-size");
		 data_refresh = $(this).attr("data-refresh");
		if(data_size=='') { data_size = "autoxauto"; }
		var size = data_size.split('x');
		
 
        if ($('#lightbox').length > 0) { // #lightbox exists
 
            //place href as img src value
			if(data_type=="image") {
         	   $('#content-lightbox').html('<img src="' + data + '" width="'+size[0]+'" height="'+size[1]+'"/>');
			    $("#lightbox-box").css("width", size[0]+"px");
					   
			}
			if(data_type=="iframe") {
         	   $('#content-lightbox').html('<iframe src="' + data + '" width="'+size[0]+'" height="'+size[1]+'"  scrolling=no frameborder=0 /></iframe>');
					   $("#lightbox-box").css("width", size[0]+"px");
			}
			if(data_type=="html") {
				if(size[0]!="auto") { size[0] = size[0]+"px"; }
				if(size[1]!="auto") { size[1] = size[1]+"px"; }
         	   $('#content-lightbox').html('<div style="width:'+size[0]+'; height:'+size[1]+'; ">'+data+'<div/>');
					   $("#lightbox-box").css("width", size[0]+"px");
			}
          
		  
            $('#lightbox').show();
        } else {
			
            var lightbox =
            '<div id="lightbox"><div id="lightbox-box">' +
                '<a href="#" class="lightbox-close" >Close</a>' +
                '<div id="lightbox-content">'; //insert clicked link's href into img src
                   
				   	if(data_type=="image") {
					  lightbox +='<img src="' + data + '" />';
         	   $('#content-lightbox').html('<img src="' + data + '" width="'+size[0]+'" height="'+size[1]+'"/>');
					  
					}
					if(data_type=="iframe") {
					   lightbox +='<iframe src="' + data + '" width="'+size[0]+'" height="'+size[1]+'"  scrolling=no frameborder=0 /></iframe>';
					}
					if(data_type=="html") {
					  lightbox +='<div style="width:'+size[0]+'px; height:'+size[1]+'px; ">'+data+'<div/>';
					   
					}
				   
				   
                lightbox +='</div>' +
            '</div></div>';
 
			$('.lightbox-close').live('click', function(e) {  e.preventDefault(); });
            //insert lightbox HTML into page
            $('body').append(lightbox);
			$("#lightbox-box").css("width", size[0]+"px");
        }
		
		var hg1 = Math.round( ($(window).height()-$("#lightbox-box").height())/2 );
		if(hg1<0) { hg1 = 10; }
		
		$("#lightbox-box").css("margin-top", hg1);
		
 
    });
	//Click anywhere on the page to get rid of lightbox window
    $('#lightbox').live('click', function() { //must use live, as the lightbox element is inserted into the DOM
        $('#lightbox').hide();
		//alert("ok1");
	//	var data_refresh = $('#lightbox').attr("data-refresh");
		if(data_refresh=="true"||data_refresh==true) {
		//	alert("ok");
			 $('#lightbox').remove();			
		}
    });
 
});



--------------------------------- HTML -------------------------------



<a href="#" class="lightbox_trigger" data-type="iframe" data-refresh="true" data-size="450x200"> OBJET-LIEN </a>



--------------------------------- CSS ---------------------------------



@charset "UTF-8";
/* CSS Document */

body.popup {
	background-image: none;
	background-color: #FFFBEF;
}

#lightbox {
    position:fixed; /* keeps the lightbox window in the current viewport */
    top:0;
    left:0;
    width:100%;
    height:100%;
	background-color:rgba(0,0,0,0.5);
	display:block;
    text-align:center;
	z-index: 10000;
}

#lightbox-box {
	display:block;
	margin-left:auto;
	margin-right:auto;
    box-shadow:0 0 10px #666666;
    -webkit-box-shadow:0 0 10px #666666;
    -moz-box-shadow:0 0 10px  #666666;
	padding:5px;
	-webkit-border-radius: 10px;
	-moz-border-radius: 10px;
	border-radius: 10px;
}
#lightbox- img {
}

/* Personalised configuration */

#lightbox-box {
	background-repeat:repeat-x;
	background-color:#FFFBEF;
}

.lightbox-close, .lightbox-close:hover {
	margin-top:5px;
	margin-right:5px;
	float:right;
}

#content-lightbox {
	background-color: #FFFBEF;
	text-align: justify;
	width: 425px;
	position:inherit;
	padding: 15px 5px 5px 5px;
}
#content-lightbox p  {
	 margin: 0 !important;
}	

a.lightbox_trigger {
	color: #9CC11C !important;
}
