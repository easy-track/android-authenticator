# ET_Authenticator (ET User and Data Management using gRPC and Google ID login)
<h3>Step 1: Ask the user to install the "EasyTrack Authenticator" application</h3>
<code>
@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  setContentView(R.layout.activity_authentication);
  
  if (authAppIsNotInstalled()) {
    Toast.makeText(this, "Please install the EasyTrack Authenticator, close the app, and reopen your application!", Toast.LENGTH_SHORT).show();
    Intent intent = new Intent(Intent.ACTION_VIEW);
    intent.setData(Uri.parse("https://play.google.com/store/apps/details?id=inha.nslab.easytrack"));
    intent.setPackage("com.android.vending");
    startActivity(intent);
  }
}
private boolean authAppIsNotInstalled() {
  try {
    getPackageManager().getPackageInfo("inha.nslab.easytrack", 0);
    return false;
  } catch (PackageManager.NameNotFoundException e) {
    return true;
  }
}
</code>

<h3>Step 2: Launch the EasyTrack Authenticator</h3>
<code>
Intent launchIntent = getPackageManager().getLaunchIntentForPackage("inha.nslab.easytrack");
if (launchIntent != null) {
  launchIntent.setFlags(0);
  startActivityForResult(launchIntent, RC_OPEN_ET_AUTH);
}
</code>

<h3>Step 3: Get the result from the EasyTrack Authenticator</h3>
<code>
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
  super.onActivityResult(requestCode, resultCode, data);
  if (requestCode == RC_OPEN_ET_AUTH) {
    if (result data != null) {
      if (resultCode == Activity.RESULT_OK) {
        String idToken = data.getStringExtra("idToken");
        String fullName = data.getStringExtra("fullName");
        String email = data.getStringExtra("email");
        int userId = data.getIntExtra("userId", -1);
        // YOUR CODE HERE
      } else if(resultCode == Activity.RESULT_FIRST_USER) {
        // User canceled
        // YOUR CODE HERE
      } else if(resultCode == Activity.RESULT_CANCELED) {
        // Failure occurred (network unavailable, etc.)
        // YOUR CODE HERE
      }
    }
}
</code>

<style>
code {
  display: block;
  white-space: pre-wrap;
}
</style>