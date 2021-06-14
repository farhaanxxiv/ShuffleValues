<!DOCTYPE html>



<html lang="en">


<head>

    <title>ChitWithName</title>
    <link rel="stylesheet" href="project.css">


</head>



<body>

    <script type="text/javascript"
        src="https://unpkg.com/jspdf-autotable@3.5.13/dist/jspdf.plugin.autotable.js"></script>

    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/1.3.2/jspdf.min.js"></script>


    <script>

        function download_DIVPdf(divid) {
            var pdf = new jsPDF('p', 'pt', 'letter');
            var pdf_name = 'PostMode-.pdf';
            // source can be HTML-formatted string, or a reference
            // to an actual DOM element from which the text will be scraped.
            htmlsource = document.getElementById(divid);

            specialElementHandlers = {
                // element with id of "bypass" - jQuery style selector
                '#bypassme': function (element, renderer) {
                    // true = "handled elsewhere, bypass text extraction"
                    return true
                }
            };
            margins = {
                top: 80,
                bottom: 60,
                left: 40,
                width: 522
            };

            pdf.fromHTML(
                htmlsource, // HTML string or DOM elem ref.
                margins.left, // x coord
                margins.top, { // y coord
                'width': margins.width, // max width of content on PDF
                'elementHandlers': specialElementHandlers
            },

                function (dispose) {

                    pdf.save(pdf_name);
                }, margins);
        }
    </script>


    <h1>Random Table Generator</h1>
	<h2>Takes input and then shuffles values in the 2nd table.</h2>
	<h3>If there are less number of inputs in Table 2 than table 1. It will multiply inputs of Table 2 to match with Table 1  </h3>
	
	<h3>Click Create below the tables for a quick demo.</h3>
	<h3>You can download the table in the form of pdf by clicking on Download as PDF</h3>




    <br><br><br><br>


    <div class="cwninputclass">

        <div class="rollnumbers">
            <h2 style="margin-left: 100px;" class="nvm-headings">Heading:</h2>
            <input id="inputhead1" type="text" style="margin-left: 100px;" value = 'Serial.No.'/><br><br>
            <textarea id="inputarea1" name="w3review" rows="20" cols="40"
                style="font-size:larger;margin-left:100px; height: auto;">1
2
3
4
5
6
7
8
9
10</textarea>
        </div>

        <div class="topics">
            <h2 class="nvm-headings" style="margin-left: 50px;">Heading:</h2>
            <input id="inputhead2" type="text" style="margin-left: 50px;" value = 'Names' /><br><br>
            <textarea id="inputarea2" name="w3review" rows="20" cols="40"
                style="font-size:larger;margin-left: 50px; height: auto;">Syed
Farhaan 
Yousuf
Safan
Afnan
Faizan
Fardeen
Shaaz
King
Queen</textarea>

        </div>

        <div style="clear:both;"></div>

    </div>

    <a href="#finaltable"> <button type="button" onclick="getNames()" id="createButton">Create</button></a>


    <div id="finaltable">

    </div>
	
	
	
	
	<h3>First Create then Download as PDF</h3>


    <script>


        function addToTable() {


            document.getElementById("finaltable").innerHTML = "";


            var head1 = document.getElementById("inputhead1").value;
            var head2 = document.getElementById("inputhead2").value;

            var table1data = document.getElementById("inputarea1").value;

            array = table1data.split("\n");

            var array1 = array.filter(function (str) {
                return /\S/.test(str);
            });

            var table2data = document.getElementById("inputarea2").value;

            array2 = table2data.split("\n");

            var array3 = array2.filter(function (str) {
                return /\S/.test(str);
            });


            if (array3.length < array1.length) {

                var times = array1.length - array3.length;

                for (var i = 0; i < times; i++) {

                    array3.push(array3[i]);

                }

            }

            shuffleArray(array3);



            var mytable = '<p class  = "yourTable">Your Table:<br></p><table id = "outputtable"><tr><th>' + head1 + "</th><th>" + head2 + "</th></tr>";

            for (var i = 0; i < array1.length; i++) {
                mytable += "<tr><td>" + array1[i] + "</td><td>" + array3[i] + "</tr>";
            }

            mytable += "</table>";
            document.getElementById("finaltable").insertAdjacentHTML('afterbegin', mytable);


        }

        function shuffleArray(array) {
            for (var i = array.length - 1; i > 0; i--) {
                var j = Math.floor(Math.random() * (i + 1));
                var temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }

        function getNames() {

            addToTable();
            /* var x = document.getElementById("w3review").value;
 
             var array = [];
             array = x.split("\n");
 
             array1 = array.filter(function (str) {
                 return /\S/.test(str);
             });
 
             //document.getElementById("test").textContent = array1;
             console.log(array1);*/




        }

        document.cookie = "totalInputs=" + 0;

        document.addEventListener('keydown', function (event) {
            //  if (event.keyCode == 13) {
            // alert('Left was pressed');
            // load();
            // }
        });

        function load() {
            // var y =  0;
            var x = document.getElementById("cwninput").value;

            if (x == "") {

                alert("Please Enter A Value");

            } else {

                var cookie = ("; " + document.cookie).split("; totalInputs=").pop().split(";").shift();

                var total = parseInt(x) + parseInt(cookie);
                // alert(total);

                document.getElementById("test").textContent = "Total Input: " + total;

                document.cookie = "totalInputs=" + total;
            }
            //var totalInput = x+y;


            //---------------------------------------------------------

            var i;
            for (i = 1; i <= x; i++) {

                var p = '<input id ="name" style = "margin-top:20px; margin-left:50px;" ' + i + ' /><br>';


                document.getElementById("form").insertAdjacentHTML('afterend', p);


            }

        }

    </script>




    <div id="finaltable"></div>
	
	

    <button id= 'createButton' type="button"  class = 'btn-pdf' onclick="download_DIVPdf('finaltable');">Download AS PDF</button>



</body>


</html>
