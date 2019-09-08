# NLP
{% extends "bootstrap/base.html" %}

{% block content %}

<style type="text/css">
		body{
	font:15px/1.5 Arial, Helvetica,sans-serif;
}
		.spinner-1:before{
			content: "";
			box-sizing: border-box;
			position: absolute;
			top:50%;
			left: 50%;
			height: 60px;
			width: 60px;
			margin-top: -30px;
			margin-left: -30px;
			border-radius: 50%;
			border:6px solid transparent;
			border-top-color: #0091EA;
			animation: spinner 0.7s linear infinite;
		}
		@keyframes spinner {
			to {
				transform: rotate(360deg);
			}
		}
		li { background-color:#BDBDBD; }
		li:nth-child(odd) { background-color:#0091EA; }
		</style>


<div class="container">
	<div class="jumbotron text-center">
		<h3>Natural Language Processing App</h3>
		<p>Understanding Everyday Language</p>
	</div>
</div>

<div class="container">
	<form method="POST" action="{{ url_for('analyse')}}" id="myForm">
		

		<label >Enter Your Text Below</label>
    <textarea class="form-control" rows="3" cols="2" name="rawtext"></textarea>

    <input type="submit" onclick="myAnalyser()" value="Submit" class="btn btn-primary ">
    <input type="button" onclick="myFunction()" value="Clear" class="btn btn-outline-dark">

    <a href="{{ url_for('index')}}" type="button" class="btn btn-danger" > Reset</a>
    
	</form>
	
</div>
<br/>
<hr/>
<div class="main">
<div class="container">
	<div class="card">
  <div class="card-header">
    Main Points
  </div>
  <div class="card-body">
    <h5 class="card-title"><div class="alert alert-primary" role="alert">
  This text has {{number_of_tokens}} tokens with {{len_of_words}} important point
</div> </h5>
    <div class="card-text"> 
    	<h5>Your Text</h5>
    	<p style="color:#0091EA;font-family:sans-serif;">{{ received_text }}</p>
    	<hr/>
<br/>
<p>Time Elapsed: <span style="color:#0091EA;">{{ final_time }} </span> seconds to analyse</p>
    <p>This text is about:</p>
    {% for i in summary %}
    <ul class="list-group ">
    	<li class="list-group-item list-group-item-info"><span style="color:black">{{i}}</span>
    		<a href="http://www.dictionary.com/browse/{{i}}?s="  target="_blank" type="button" class="btn btn-outline-primary btn-sm" style="float:right;font-size:9px;color:#fff;">View</a>
    		
    	</li>
    </ul>
	

	{% endfor %}
  </div>
  <div class="card-footer text-muted">
  <table class="table table-striped table-dark" >
  <thead>
    <tr>
      <th scope="col">Sentiment</th>
      <th scope="col">Polarity</th>
      <th scope="col">Subjectivity</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Score:</th>
      <td>{{blob_sentiment}}</td>
      <td>{{blob_subjectivity}}</td>
    </tr>
</tbody></table>

</div>

	
</div>
</div>


{% endblock %}









<!-- Scripts starts here -->
{% block scripts %}

{{ super() }}

<script>
function myFunction() {
    document.getElementById("myForm").reset();
}
</script>
<script>
function myAnalyser() {
    document.querySelector('.main div').style.display = 'none';
	//Hide the main division
	document.querySelector('.main').classList.add('spinner-1');
	// Server request
	setTimeout(() => {
	document.querySelector('.main').classList.remove('spinner-1');
	//Remove the animation
	document.querySelector('.main div').style.display = 'block';
	//Show the main division
	},5000);//Number of seconds to last
}
</script>

<!-- Prevent it from being overwritten -->

{% endblock %}
