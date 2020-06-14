# jquery_basics
### all the ids,classes and tags are just for understanding the code
<pre><code>$(function () {

// fades

$(".red-box").fadeOut(1000);
$(".green-box").fadeOut(2000);
$(".blue-box").fadeOut(3000);
$(".blue-box").fadeIn(1000);
$(".green-box").fadeIn(1000);
$(".red-box").fadeIn(1000);
$(".red-box").fadeTo(1000, 0.2);
$(".green-box").delay(1000).fadeTo(1000, 0.4);
$(".blue-box").delay(2000).fadeTo(1000, 0.6).fadeOut().delay(500).fadeIn();
$(".green-box").fadeToggle(1000);


// hide/show

$(".green-box").show();
$(".green-box").hide(1000);
$(".green-box").toggle();
// slidesUp/Down
$(".green-box").slideUp(2000);
$(".green-box").slideDown(2000);
$("p").show();
$("p").slideDown(2000);
$("p").slideToggle(2000);


// animations

$(".blue-box").animate(
  {
    "margin-left": "+=200px",
  },
  2000,
  "linear"
);
  $(".blue-box").animate(
    {
      "margin-left": "-=200px",
    },
    2000,
    "linear"
  );
$(".blue-box").animate(
  {
    "margin-left": "+=200px",
    opacity: "0",
    height: "50px",
    width: "50px",
    "margin-top": "+=25px",
  },
  1000
);



// css selector

$("p").css("background-color", "rgba(180,180,30,0.8)");
$("input[type=text]").css("background-color", "rgba(180,180,30,0.8)");
$("input:text").css("background-color", "rgba(180,180,30,0.8)");
$("p,h1,input").css("background-color", "rgba(180,180,30,0.8)");
$("p").css("background-color", "rgba(180,180,30,0.8)");
$("li:last").css("background-color", "rgba(180,180,30,0.8)");
$("li:odd").css("background-color", "rgba(180,180,30,0.8)");
$("select").css("background-color", "rgba(180,180,30,0.8)");



// jquery methods for treversal

$("#list").find("li").css("background-color", "rgba(180,180,30,0.8)");
$("#list").children("li").css("background-color", "rgba(180,180,30,0.8)");
$("#list").parents().css("background-color", "rgba(180,180,30,0.8)");
$("#list").parent().css("background-color", "rgba(180,180,30,0.8)");
$("#list")
  .siblings(":header")
  .css("background-color", "rgba(180,180,30,0.8)");
$("#list").prev().css("background-color", "rgba(180,180,30,0.8)");
$("#list").next().css("background-color", "rgba(180,180,30,0.8)");



// jquery filtering

$("#list").children("li").filter(":even").css("background-color", "rgba(180,180,30,0.8)");
$("li")
  .filter(function (index) {
    return index % 3 == 2;
  })
  .css("background-color", "rgba(180,180,30,0.8)");
$("li").first().css("background-color", "rgba(180,180,30,0.8)");
$("li").last().css("background-color", "rgba(180,180,30,0.8)");
$("li").eq(-2).css("background-color", "rgba(180,180,30,0.8)");
$("li").not(":even").css("background-color", "rgba(180,180,30,0.8)");



// adding new Element to the dom

$("ul ul:first").append("<li>hello threre</li>");
$("ul ul:first").prepend("<li>hello threre</li>");
$("<li>hello threre</li>").appendTo("ul ul");
$("<li>hello threre</li>").prependTo("ul ul");
$("#list").before("<div>shubham sharma</div>");
$("#list").after("<div>shubham sharma</div>");
$(".red-box").after("  <div class='red-box'>red 2</div>");



// replacing elements

let green = $(".green-box");
$(".red-box, .blue-box").replaceWith(green);
// remove element
$("form").children().not("textarea,input:text,br").remove();
$("li").detach();
$(".red-box,.green-box,.blue-box").empty();



// attr, prop, val

let link = $(".link");
// get href value
link.attr("href");
// replace href value
link.attr("href","google.com");
$(".checkbox").prop("checked");
$("input:text").val();



// adding classes and removing

$("a").addClass("fancy-link");
$("a").removeClass("fancy-link");


// content of element
var firstPar = $("p:first");
firstPar.text("<strong>hello</strong>world!");
firstPar.html(firstPar.html() + "<strong>hello</strong> world!");
});



// image gallary

$(() => {
  let gallaryImages = $(".gallary").find("img");
  let imgArr = ["./images/1.jpg", "./images/2.jpg", "./images/3.jpg"];
  let i = 0;
  setInterval(() => {
    i = (i + 1) % imgArr.length; //0 1 2 0 1 2....
    gallaryImages.fadeOut(() => {
      gallaryImages.attr("src", imgArr[i]);
      gallaryImages.fadeIn();
    });
  }, 2000);
});




//event listners

$(function () {
let box = $(".red-box");
box.click(() => {
  box.fadeTo(1000, 0.5);
});
let box = $(".green-box");
box.hover(() => {
  box.text("i was hovered");
});
let box = $(".green-box");
box.hover(
  () => {
    //for mouseenter
    box.stop().fadeTo(500, 0.5);
  },
  () => {
    //for mouseleave
    box.stop().fadeTo(500, 1);
  }
);
let imgArr = ["./images/1.jpg", "./images/2.jpg", "./images/3.jpg"];
let i = 0;
$(".gallary")
  .find("img")
  .on("click", function () {
    i = (i + 1) % imgArr.length;
    $(this).fadeOut(function () {
      $(this).attr("src", imgArr[i]).fadeIn();
    });
  });
});



$(function () {
  //event delegation
  $("body").on("click", "li", function (e) {
    e.target.parentElement.remove();
    console.log(e.target);
  });

  //add data to event
  $("input:submit").click({ name: "shubham" }, function (e) {
    alert(e.data.name);
    e.preventDefault();
  });
});




//image gallary which can be used as light box

$(function () {
  let gallaryImages = $(".gallary").find("img");
  gallaryImages.css("width", "33%").fadeTo(200, 0.7);
  gallaryImages.mouseenter(function () {
    $(this).stop().fadeTo(500, 1);
  });
  gallaryImages.mouseleave(function () {
    $(this).stop().fadeTo(500, 0.7);
  });

// adding to lightbox
gallaryImages.click(function () {
  let source = $(this).attr("src");
  let image = $("<img>").attr("src", source).css("width", "100%");
  $(".lightbox").empty().append(image).fadeIn(2000);
});
$(".lightbox").click(function () {
  $(this).stop().fadeOut();
});
});




//working with forms

$(function () {
  //focus and blur event
  let inputfields = $("input:text,textarea");
  inputfields.focus(function () {
    $(this).css("box-shadow", "0 4px 4px #666");
  });
  inputfields.blur(function () {
    $(this).css("box-shadow", "none");
  });

// validation
$("#textarea").blur(function () {
  let temp = $(this).val();
  if (temp.length < 3) {
    $(this).css("box-shadow", "0 4px 4px #811");
  } else {
    $(this).css("box-shadow", "0 4px 4px #183");
  }
});




// change element

$("#selection").change(function () {
  var selector = $(this).find(":selected").text();

  alert(selector);
});




// handling submit event

  $("form").submit(function (e) {
    var textarea = $("textarea");
    if (textarea.val().trim() == "") {
      textarea.css("box-shadow", "0 4px 4px #811");
      e.preventDefault();
    }
  });
});




//complete form validation on submit

$(function () {
  $("#form").submit(function (e) {
    const name = $("#name").val();
    const password = $("#password").val();
    const message = $("#textarea").val();
    const cheacked = $("#checkbox").is(":checked");
    validatenamefield(name, e);
    validatepasswordfield(password, e);
  });
});

function validatenamefield(name, e) {
  if (!isvalidname(name)) {
    $("#name-feedback").text("please eneter at least two characters");
    e.preventDefault();
  } else {
    $("#name-feedback").text("");
  }
}
function validatepasswordfield(password, e) {
  if (!isvalidpassword(password)) {
    $("#password-feedback").text("please eneter at least two characters");
    e.preventDefault();
  } else {
    $("#password-feedback").text("");
  }
}
function isvalidname(name) {
  return name.length >= 2;
}

function isvalidpassword(password) {
  return password.length >= 3;
}




//WORKING WITH AJAX

//$.get(),$.getJSON(),$.ajax() ,load()
$(function () {
  // $("#code").load("js/app.js");
  $("#code").load("jss/app.js", function (response, status) {
    if (status == "error") {
      alert("could not find");
    }
  });
});
</code></pre>
