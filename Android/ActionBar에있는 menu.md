// Do 2 - 7 in menu.xml ///////////////////////////////////////////////////////////////////////
    // TODO (2) Create a menu xml called 'main.xml' in the res->menu folder
    // TODO (3) Add one menu item to your menu
    // TODO (4) Give the menu item an id of @+id/action_search
    // TODO (5) Set the orderInCategory to 1
    // TODO (6) Show this item if there is room (use app:showAsAction, not android:showAsAction)
    // TODO (7) Set the title to the search string ("Search") from strings.xml
    // Do 2 - 7 in menu.xml ///////////////////////////////////////////////////////////////////////

<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:title="@string/search"
        android:orderInCategory="1"
        app:showAsAction="ifRoom"
        android:id="@+id/action_search"/>
</menu>

// TODO (8) Override onCreateOptionsMenu
// TODO (9) Within onCreateOptionsMenu, use getMenuInflater().inflate to inflate the menu
// TODO (10) Return true to display your menu

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main, menu);
        return true;
    }
    
// TODO (11) Override onOptionsItemSelected
// TODO (12) Within onOptionsItemSelected, get the ID of the item that was selected
// TODO (13) If the item's ID is R.id.action_search, show a Toast and return true to tell Android that you've handled this menu click
// TODO (14) Don't forgot to call .show() on your Toast
// TODO (15) If you do NOT handle the menu click, return super.onOptionsItemSelected to let Android handle the menu click


    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        int menuItemThatWasSeelcted = item.getItemId();
        if(menuItemThatWasSeelcted == R.id.action_search){
            Context context = MainActivity.this;
            String message = "Search clicked";
            Toast.makeText(context, message, Toast.LENGTH_LONG).show();
        }
        return super.onOptionsItemSelected(item);
    }
