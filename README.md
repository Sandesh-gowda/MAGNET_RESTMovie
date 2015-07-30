# MAGNET_RESTMovie
Using open source magnet facility for fascinatingly easy REST calls

So hi there we have used all java classes and gson jackson libraries to call the REST API so   
here there is a new way of calling a REST API which is much more simpler and efficient i have   
described the main call object as there documentation says only about configuration i am taking   
it to next level with code analogy and description.

```sh

package com.ashokslsk.movielist;

import android.os.Bundle;
import android.support.v7.app.ActionBarActivity;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.ListView;

import com.ashokslsk.movielist.controller.api.RTMovie;
import com.ashokslsk.movielist.controller.api.RTMovieFactory;
import com.ashokslsk.movielist.model.beans.MoviesResult;
import com.magnet.android.mms.MagnetMobileClient;
import com.magnet.android.mms.async.Call;
import com.magnet.android.mms.exception.SchemaException;

import java.util.List;
import java.util.concurrent.ExecutionException;


public class MainActivity extends ActionBarActivity {
  
  // Mandatory declaration where controllerFactory gets refernce in  
    private RTMovie movie;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        // Rest Call using Magnet network service client
        MagnetMobileClient magnetClient = MagnetMobileClient.getInstance(getApplicationContext());
        
        // defining URL POJO FACTORIES
        RTMovieFactory controllerFactory = new RTMovieFactory(magnetClient);
        try {
            movie = controllerFactory.obtainInstance();
        } catch (SchemaException e) {
            e.printStackTrace();
        }
        // ACTUAL WEB SERVICE CALLS and the callObject returns all the JSON nodes.
        Call<List<MoviesResult>> callObject = movie.getMovies(null);

        try {
        
            // SO this is as usual that easy to add it to your list view with the custom adapter
            List<MoviesResult> result = (List<MoviesResult>) callObject.get();
            final ListView listview = (ListView) findViewById(R.id.list);

            CustomListAdapter earthAdapter = new CustomListAdapter(MainActivity.this,result);

            listview.setAdapter(earthAdapter);

        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }
}


```

This following image is the result after using magnet library to call the API.
![Screen](https://github.com/ashokslsk/MAGNET_RESTMovie/blob/master/Magnet%20Rest%20parsing/MovieList/screen/screen.png)

You can actually find there configuration documentation on the following link.
[MAGNET SDK](https://docs.magnet.com/rest2mobile/setup-for-android/)

After this configuration your REST calls must be easier to call and simpler to analyse.



Finally your done now.

- Execute it as simple as it is 

* [For more codes, funs and for queries be in touch with @ashokslsk ](https://github.com/ashokslsk)



