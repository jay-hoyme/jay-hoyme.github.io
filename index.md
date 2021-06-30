<style type='text/css'>
    .embeddedServiceHelpButton .helpButton .uiButton {
        background-color: #005290;
        font-family: "Arial", sans-serif;
    }
    .embeddedServiceHelpButton .helpButton .uiButton:focus {
        outline: 1px solid #005290;
    }
</style>
<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
    var initESW = function(gslbBaseURL) {
        embedded_svc.settings.displayHelpButton = true; //Or false
        embedded_svc.settings.language = ''; //For example, enter 'en' or 'en-US'
        //embedded_svc.settings.defaultMinimizedText = '...'; //(Defaults to Chat with an Expert)
        embedded_svc.settings.disabledMinimizedText = 'No Agents Available'; //(Defaults to Agent Offline)
        //embedded_svc.settings.loadingText = ''; //(Defaults to Loading)
        //embedded_svc.settings.storageDomain = 'yourdomain.com'; //(Sets the domain for your deployment so that visitors can navigate subdomains during a chat session)
        // Settings for Chat
        embedded_svc.settings.directToButtonRouting = function(prechatFormData) {
            // Dynamically changes the button ID based on what the visitor enters in the pre-chat form.
            // Returns a valid button ID.    
            if (prechatFormData[5].value=="Your HSOne Invoice")
                return "5734v0000008kQV";
            else if (prechatFormData[4].value=="Dentrix")
                return "5734v0000008kQa";
            else if (prechatFormData[4].value=="Patient Engage")
                return "5734v0000008kQu";
            else if (prechatFormData[4].value=="eServices")
                return "5734v0000008kQp";
            else if (prechatFormData[4].value=="ePrescribe")
                return "5734v0000008kQz";    
            else if (prechatFormData[4].value=="IHS")
                return "5734v0000008kR4";        
            else if (prechatFormData[4].value=="Dentrix Enterprise")
                return "5734v0000008kQf";
            else if (prechatFormData[4].value=="Specialty")
                return "5734v0000008kQk";
            else if (prechatFormData[4].value=="Ascend")
                return "5734v0000008kQQ";
            else {return "5734v0000008kQa";}
};
        //embedded_svc.settings.prepopulatedPrechatFields = {}; //Sets the auto-population of pre-chat form fields
        //embedded_svc.settings.fallbackRouting = []; //An array of button IDs, user IDs, or userId_buttonId
        //embedded_svc.settings.offlineSupportMinimizedText = '...'; //(Defaults to Contact Us)
        embedded_svc.settings.enabledFeatures = ['LiveAgent'];
        embedded_svc.settings.entryFeature = 'LiveAgent';
        embedded_svc.init(
            'https://henryscheinone.my.salesforce.com',
            'https://hsione.force.com/dentrixenterprise',
            gslbBaseURL,
            '00D1U0000014Tc8',
            'Support_Chat_Core',
            {
                baseLiveAgentContentURL: 'https://c.la2-c2-ia5.salesforceliveagent.com/content',
                deploymentId: '5723t000000TtGm',
                buttonId: '5733t000000Turo',
                baseLiveAgentURL: 'https://d.la2-c2-ia5.salesforceliveagent.com/chat',
                eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04I4v000000fxTnEAI_17a1aca0e3c',
                isOfflineSupportEnabled: false
            }
        );
    };
    if (!window.embedded_svc) {
        var s = document.createElement('script');
        s.setAttribute('src', 'https://henryscheinone.my.salesforce.com/embeddedservice/5.0/esw.min.js');
        s.onload = function() {
            initESW(null);
        };
        document.body.appendChild(s);
    } else {
        initESW('https://service.force.com');
    }
</script>
