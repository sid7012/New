<!DOCTYPE html>
<!--
To change this license header, choose License Headers in Project Properties.
To change this template file, choose Tools | Templates
and open the template in the editor.
-->
<html lang="en">
    <head>
        <title>Bootstrap Example</title>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="stylesheet"
              href="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/css/bootstrap.min.css">
        <script
        src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
        <script
        src="https://maxcdn.bootstrapcdn.com/bootstrap/3.4.1/js/bootstrap.min.js"></script>
    </head>
    <body>
        <div class="container">
            <h2>Student Enrollment Form</h2>
            <form id="empForm" method="post">
                <div class="form-group">
                    <span><label for="empId">Roll No:</label> <label id="empIdMsg">
                        </label></span>
                    <input type="text" class="form-control" name="empId" id="empId"
                           placeholder="Enter Roll No" required>

                </div>
                <div class="form-group">
                    <label for="empName">Full Name:</label>
                    <input type="text" class="form-control" id="empName"
                           placeholder="Enter Full Name" name="empName">
                </div>
                <div class="form-group">
                    <label for="empClass">Class:</label>
                    <input type="Class" class="form-control" id="empClass"
                           placeholder="Enter Class" name="empClass">
                </div>

                <div class="form-group">
                    <label for="empName">Birth Date:</label>
                    <input type="text" class="form-control" id="empName"
                           placeholder="Enter Birth Date" name="empName">
                </div>
                <div class="form-group">
                    <label for="empName">Address:</label>
                    <input type="text" class="form-control" id="empName"
                           placeholder="Enter Address" name="empName">
                </div>
                <div class="form-group">
                    <label for="empName">Enrollment Date:</label>
                    <input type="text" class="form-control" id="empName"
                           placeholder="Enter Enrollment" name="empName">
                </div>
                <input type="button" class="btn btn-primary" id="empSave" value="Save"
                       onclick="saveEmployee();">
                <input type="button" class="btn btn-primary" id="empChange" value="Change"
                       onclick="changeData();">
                <input type="button" class="btn btn-primary" id="empSave" value="Reset"
                       onclick="resetForm();">
            </form>
        </div>

        <script>


            function validateAndGetFormData() {
            var empIdVar = $("#empId").val();
            if (empIdVar === "") {
            alert("Roll No Required Value");
            $("#empId").focus();
            return "";
            }
            var empNameVar = $("#empName").val();
            if (empNameVar === "") {
            alert("Student Name is Required Value");
            $("#empName").focus();
            return "";
            }
            var empEmailVar = $("#empEmail").val();
            if (empEmailVar === "") {
            alert("Student Class is Required Value");
            $("#empEmail").focus();
            return "";
            }
            }
            var empEmailVar = $("#empEmail").val();
            if (empEmailVar === "") {
            alert("Student Birth Date is Required Value");
            $("#empEmail").focus();
            return "";
            }
            var jsonStrObj = {
            empId: empIdVar,
                    empName: empNameVar,
                    empEmail: empEmailVar,
            };
            return JSON.stringify(jsonStrObj);
            }// This method is used to create PUT Json request.
            function createPUTRequest(connToken, jsonObj, dbName, relName) {
            var putRequest = "{\n"
                    + "\"token\" : \""
                    + connToken
                    + "\","
                    + "\"dbName\": \""
                    + dbName
                    + "\",\n" + "\"cmd\" : \"PUT\",\n"
                    + "\"rel\" : \""
                    + relName + "\","
                    + "\"jsonStr\": \n"
                    + jsonObj
                    + "\n"
                    + "}";
            return putRequest;
            }

            function executeCommand(reqString, dbBaseUrl, apiEndPointUrl) {
            var url = dbBaseUrl + apiEndPointUrl;
            var jsonObj;
            $.post(url, reqString, function (result) {
            jsonObj = JSON.parse(result);
            }).fail(function (result) {
            var dataJsonObj = result.responseText;
            jsonObj = JSON.parse(dataJsonObj);
            });
            return jsonObj;
            }
            function resetForm() {
            $("#empId").val("")
                    $("#empName").val("");
            $("#empEmail").val("");
            $("#empId").focus();
            }
            function saveEmployee() {
            var jsonStr = validateAndGetFormData();
            if (jsonStr === "") {
            return;
            }
            function changeData() {
            var jsonStr = validateAndGetFormData();
            if (jsonStr === "") {
            return;
            }
            var putReqStr = createPUTRequest("90938317|-31949273677770249|90952324",
                    jsonStr, "SAMPLE", "EMP-REL");
            alert(putReqStr);
            jQuery.ajaxSetup({async: false});
            var resultObj = executeCommand(putReqStr,
                    "http://api.login2explore.com:5577", "/api/iml");
            alert(JSON.stringify(resultObj));
            jQuery.ajaxSetup({async: true});
            // resetForm();
            }
        </script>
    </body>
</html>
