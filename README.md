# UMUX Popup

Integrate a simple popup for usability evaluation into WordPress. The actual survey needs to be handled externally, e.g. using https://www.limesurvey.org/. We use UMUX at Stabi Berlin, but you can use any metric you like.

Add the following code to the functions.php:

```js
// Add UMUX Survey
function umux(){
    ?>
<script>
  <!-- UMUX Popup -->
  (function () {
    // Configuration for the UMUX-Feedback-Popup
    window.UMUXConfig = {
      surveyUrl:
        "https://{$LIMESURVEY_URL}/index.php/{$LIMESURVEY_ID}?lang=de",
      popupWidth: 800,
      popupHeight: 600,
      triggerText: "Feedback",
      popupCloseText: "Close",
      cssUrl: "https://3zm75f.csb.app/umux-popup.css",
    };

    // Dynamisch die JavaScript-Datei laden
    const script = document.createElement("script");
    script.src = "https://3zm75f.csb.app/umux-popup.js";
    script.type = "text/javascript";
    script.async = true;

    script.onload = function () {
      console.log("UMUX Popup Script ready.");
    };

    script.onerror = function () {
      console.error("Error loading the UMUX Popup Scripts.");
    };

    document.head.appendChild(script);
  })();
  <!-- End UMUX Popup -->
</script>
    <?php
}
add_action('wp_body_open', 'umux');
```

If you use Enfold as your WordPress theme, add the icon via Fontello in the Theme Options.
