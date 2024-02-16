<script type='text/javascript'>
	function initEmbeddedMessaging() {
		try {
			embeddedservice_bootstrap.settings.language = 'en_US'; // For example, enter 'en' or 'en-US'

			embeddedservice_bootstrap.init(
				'00D6g000000D5Hr',
				'Help_Center_Web_Messaging',
				'https://workstream.my.site.com/ESWHelpCenterWebMessag1697042361989',
				{
					scrt2URL: 'https://workstream.my.salesforce-scrt.com'
				}
			);
		} catch (err) {
			console.error('Error loading Embedded Messaging: ', err);
		}
	};
</script>
<script type='text/javascript' src='https://workstream.my.site.com/ESWHelpCenterWebMessag1697042361989/assets/js/bootstrap.min.js' onload='initEmbeddedMessaging()'></script>
