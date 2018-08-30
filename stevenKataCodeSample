 //stevenKataCodeSample.js
 
var sitterStart, sitterQuit, sleepTime, payOut, amShift$, midShift$, pmShift$;

var midnight = 7;

//Pay rate from 5pm to sleepTime
var earlyRate = 12;
//Pay rate from sleepTime to 12am
var midRate = 8;
//Pay rate from 12 am to 4 am
var lateRate = 16;

var $start = document.getElementById("start-time");
var $bed = document.getElementById("sleepTime");
var $end = document.getElementById("end-time");

//Converts option string value to number
function convertValue(string) {
	if (string !== "na") {
		string = parseInt(string);
	} 
	return string;
}

//Sets start time 
function getsitterStart() {
	sitterStart = $start.options[$start.selectedIndex].value;
	return sitterStart;
}

//Sets sleepTime
function getsleepTime() {
	sleepTime = $bed.options[$bed.selectedIndex].value;
	return sleepTime;
	}

//Sets end time
function getsitterQuit() {
	sitterQuit = $end.options[$end.selectedIndex].value;
	return sitterQuit;
}

//Checks if sitterStart is valid or not
function issitterStartValid(sitterStart, sitterQuit) {
	if (typeof sitterStart === 'number' && sitterStart < sitterQuit) {
		return true;
		}
		return false;
	}
	
function errorMessage() {
	return '<p>Error: The combination of times you selected is invalid. Please try again.</p>';
	}
	
//Calculates pay for shift segment
function getSegmentPay(time1, time2, payrate) {
	return (time2 - time1) * payrate;
}

//Calculates total pay
function calculateTotal(pay1, pay2, pay3) {
	return pay1 + pay2 + pay3;
}

//Sets html for results div
function showResults(pay) {
	return '<p>You will be paid $' + pay + ' for this shift.</p>';
	}

//Submit button is disabled by default
document.getElementById('submitButton').disabled = true;

//When a selection is changed
$('#start-time, #sleepTime, #end-time').change(function() {
		//If they all have values, enables button
		if ($('#start-time').val() && $('#sleepTime').val() && $('#end-time').val()) {
		document.getElementById('submitButton').disabled = false;
		} else {
      document.getElementById('submitButton').disabled = true;
    }
	});

//When submit button is clicked, the functions run	
$('#submitButton').click(function() {
	
	getsitterStart();
	getsleepTime();
	getsitterQuit();
	
	sitterStart = convertValue(sitterStart);
	sleepTime = convertValue(sleepTime);
	sitterQuit = convertValue(sitterQuit);
	
	//If start time is not valid displays error
	if (!issitterStartValid(sitterStart, sitterQuit)) {
		$(".results").html(errorMessage());
		payOut = 0;
		} 
		
		//Assigns pay for each shift dependent on times selected
	   if (sleepTime >= sitterQuit && sitterQuit > sitterStart) {
		  amShift$ = getSegmentPay(sitterStart, sitterQuit, earlyRate); 
		  midShift$ = 0;
		  pmShift$ = 0;
		 } else if (sleepTime === "na" && sitterQuit <= midnight) {
			 sleepTime = sitterQuit;
			 amShift$ = getSegmentPay(sitterStart, sitterQuit, earlyRate);
			 midShift$ = 0;
			 pmShift$ = 0;
		} else if (sleepTime > sitterStart && sitterQuit < midnight) {
			amShift$ = getSegmentPay(sitterStart, sleepTime, earlyRate);
			midShift$ = getSegmentPay(sleepTime, sitterQuit, midRate);
			pmShift$ = 0;
		} else if (sleepTime <= sitterStart && sitterQuit <= midnight) {
			amShift$ = 0;
			midShift$ = getSegmentPay(sitterStart, sitterQuit, midRate);
			pmShift$ = 0;
		} else if (sleepTime === "na" && sitterQuit > midnight) {
			amShift$ = getSegmentPay(sitterStart, midnight, earlyRate);
			midShift$ = 0;
			pmShift$ = getSegmentPay(midnight, sitterQuit, lateRate);
		} else if (sleepTime <= sitterStart && sitterQuit > midnight) {
			amShift$ = 0;
			midShift$ = getSegmentPay(sitterStart, midnight, midRate);
			pmShift$ = getSegmentPay(midnight, sitterQuit, lateRate);
			}
		  else {
			amShift$ = getSegmentPay(sitterStart, sleepTime, earlyRate);
			midShift$ = getSegmentPay(sleepTime, midnight, midRate);
			pmShift$ = getSegmentPay(midnight, sitterQuit, lateRate);
		  }
	 //Calculates total pay 
	if (payOut !== 0) {
			payOut = calculateTotal(amShift$, midShift$, pmShift$);
			$('.results').html(showResults(payOut));
		} else {
			payOut = false;
			
		}
		
});
