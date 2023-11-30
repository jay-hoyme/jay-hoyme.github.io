<style type='text/css'>
    .embeddedServiceHelpButton .helpButton .uiButton {
        background-color: #0e2152;
        font-family: "Arial", sans-serif;
    }
    .embeddedServiceHelpButton .helpButton .uiButton:focus {
        outline: 1px solid #0e2152;
    }
</style>

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
    var initESW = function(gslbBaseURL) {
        embedded_svc.settings.displayHelpButton = true; //Or false
        embedded_svc.settings.language = ''; //For example, enter 'en' or 'en-US'

        // Additional Embedded Service settings ...

        embedded_svc.settings.enabledFeatures = ['LiveAgent'];
        embedded_svc.settings.entryFeature = 'LiveAgent';

        embedded_svc.init(
			'https://prioritypdc--uat.sandbox.my.salesforce.com',
			'https://prioritypdc--uat.sandbox.my.salesforce-sites.com/digengage',
			gslbBaseURL,
			'00DE20000015Pmn',
			'Course_Coordination',
			{
				baseLiveAgentContentURL: 'https://c.la2s-core1.sfdc-lywfpd.salesforceliveagent.com/content',
				deploymentId: '5724N000000GyED',
				buttonId: '5734N000000GzEV',
				baseLiveAgentURL: 'https://d.la2s-core1.sfdc-lywfpd.salesforceliveagent.com/chat',
				eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04I4N000000KynhUAC_17ec0e19017',
				isOfflineSupportEnabled: true
			}
		);
	};

    if (!window.embedded_svc) {
        var s = document.createElement('script');
        s.setAttribute('src', 'https://prioritypdc--uat.sandbox.my.salesforce.com/embeddedservice/5.0/esw.min.js');
        s.onload = function() {
            initESW(null);
        };
        document.body.appendChild(s);
    } else {
        initESW('https://service.force.com');
    }

    // Custom logic for handling the "Start Chatting" button click
    document.addEventListener('click', function(event) {
        var targetElement = event.target;
        while (targetElement != null) {
            if (targetElement.classList.contains('embeddedServiceSidebarButton') && 
                targetElement.textContent.trim() === 'Start Chatting') {
                console.log('Start Chatting button clicked');

                var selectElement = document.getElementById("What_can_we_assist_with__c");
                if (selectElement && selectElement.options[selectElement.selectedIndex]) {
                    var selectedOption = selectElement.options[selectElement.selectedIndex];
                    console.log("Selected Option Label: " + selectedOption.text);
                    console.log("Selected Option Value: " + selectedOption.value);

                    if (['Agency ID/Member ID', 'CDE Hours', 'Certification/Recertification'].includes(selectedOption.value)) {
                        console.log('Rerouting chat!');
                        rerouteChat();
                    }
                } else {
                    console.log("Select element not found or no option is selected.");
                }
                return;
            }
            targetElement = targetElement.parentElement;
        }
    }, false);

    function rerouteChat() {
        embedded_svc.liveAgentAPI.sendMessage({
            text: "We have referred your inquiry to IAED Member Services. A Member Services representative will reach out to you shortly to provide further instructions. Please close this chat and watch for an email."
        });
        embedded_svc.liveAgentAPI.endChat();
    }
</script>
