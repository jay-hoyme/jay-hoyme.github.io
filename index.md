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
        embedded_svc.settings.displayHelpButton = true; // Or false
        embedded_svc.settings.language = ''; // For example, enter 'en' or 'en-US'

        // Add direct-to-button routing based on pre-chat form responses
        embedded_svc.settings.directToButtonRouting = function(prechatFormData) {/*
            // Iterate through pre-chat form data to find the 'What_can_we_assist_with__c' field
			console.log('In logic section');
            for (var i = 0; i < prechatFormData.length; i++) {
                if (prechatFormData[i].label === 'What_can_we_assist_with__c') {
                    var selectedOption = prechatFormData[i].value;
                    if (['Agency ID/Member ID', 'CDE hours', 'Certification/Recertification'].includes(selectedOption)) {
                        // Replace 'NEW_BUTTON_ID_FROM_SALESFORCE_SETUP' with the actual button ID you want to route to
                        return '573E2000000EOFN';
                    }
                }
            }
            // If none of the specified options were selected, return null to use the default button
            return null;*/
			console.log('in logic section');
        };

        // Other Embedded Service settings ...
        
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
</script>
