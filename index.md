<style type='text/css'>
    .embeddedServiceHelpButton .helpButton .uiButton {
        background-color: #0e2152;
        font-family: "Arial", sans-serif;
        width: 200px; /* New width */
    }
    .embeddedServiceHelpButton .helpButton .uiButton:focus {
        outline: 1px solid #0e2152;
    }
</style>

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
    console.log('initESW function is called!');
    var initESW = function(gslbBaseURL) {
        console.log('Script is running!');
        embedded_svc.settings.displayHelpButton = true;
        embedded_svc.settings.language = '';
        embedded_svc.settings.enabledFeatures = ['LiveAgent'];
        embedded_svc.settings.entryFeature = 'LiveAgent';

        // Add pre-chat field logic
        embedded_svc.settings.prechatInit = function(prechatFormData) {
            // Find the select element by its id
            var selectElement = document.getElementById("What_can_we_assist_with__c");
            console.log('selectElement: ' + selectElement);

            // Check if the select element exists and if an option is selected
            if (selectElement && selectElement.options[selectElement.selectedIndex]) {
                // Get the selected option
                var selectedOption = selectElement.options[selectElement.selectedIndex];
                console.log("Selected Option Label: " + selectedOption.text); // Use .text instead of .label
                console.log("Selected Option Value: " + selectedOption.value);

                // Reroute chat for specific selections
                if (['Agency ID/Member ID', 'CDE Hours', 'Certification/Recertification'].includes(selectedOption.value)) {
                    console.log('Rerouting chat!');
                    rerouteChat();
                    return false; // Prevent the chat from proceeding in the normal flow
                }
            } else {
                console.log("Select element not found or no option is selected.");
            }

            console.log('Prechat Form Data:', prechatFormData); // Debugging line
            return true; // Continue with the normal chat flow
        };

        function rerouteChat() {            
            // Send an auto-response message
            embedded_svc.liveAgentAPI.sendMessage({
                text: "We have referred your inquiry to IAED Member Services. A Member Services representative will reach out to you shortly to provide further instructions. Please close this chat and watch for an email."
            });
        
            // Close the chat session
            embedded_svc.liveAgentAPI.endChat();
        }

        // Initialize the embedded service
        embedded_svc.init(
            'https://prioritypdc--uat.sandbox.my.salesforce.com',
            'https://prioritypdc--uat.sandbox.my.salesforce-sites.com/digengage',
            gslbBaseURL,
            '00D54000000x1Am',
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

    // Load the embedded service script
    if (!window.embedded_svc) {
        var s = document.createElement('script');
        s.setAttribute('src', 'https://prioritypdc--uat.sandbox.my.salesforce.com/embeddedservice/5.0/esw.min.js');
        s.onload = function() {
            console.log('esw.min.js loaded successfully!');
            initESW(null);
        };
        document.body.appendChild(s);
    } else {
        initESW('https://service.force.com');
    }
</script>
