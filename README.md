# GoogleMapitasV1 
Este es un proyecto de geolocalización extremadamente básico. El primer paso es implementra las intrefaces siguientes a tu proyecto de plantilla de
de google maps:

```
//Implementar las siguientes dos interfaces
        GoogleApiClient.ConnectionCallbacks,
        GoogleApiClient.OnConnectionFailedListener {
```

 Al  hacer lo anterior te pedira implementar los métodos abstractos, al final de tu **MainActivity** verás los siguientes métodos, implementalos co el siguiente codigo.
 
```
  public void onConnected(Bundle bundle) {

        mLastLocation = LocationServices.FusedLocationApi.getLastLocation(mGoogleApiClient);
        if (mLastLocation != null) {
            Toast.makeText(this,
                    "latitud:"+ mLastLocation.getLatitude(), Toast.LENGTH_LONG).show();
            Toast.makeText(this,"Longitud"+
                    mLastLocation.getLongitude(), Toast.LENGTH_LONG).show();

            // Marcador para ecatepec
            LatLng ecatepec = new LatLng(mLastLocation.getLatitude(), mLastLocation.getLongitude());

            mMap.addMarker(new MarkerOptions().position(ecatepec)
            .title("Latitud:"+mLastLocation.getLatitude()+" Long:"+mLastLocation.getLongitude()));
            mMap.moveCamera(CameraUpdateFactory.zoomTo(18));
            mMap.moveCamera(CameraUpdateFactory.newLatLng(ecatepec));
        } else {
            Toast.makeText(this, "Localizacion no detectada", Toast.LENGTH_LONG).show();
        }

    }

    @Override
    public void onConnectionSuspended(int i) {

        mGoogleApiClient.connect();

    }

    @Override
    public void onConnectionFailed(ConnectionResult connectionResult) {

    }
 ```
 
 Posteriormente vas a declarar los siguientes dos atributos a tu **MainActivity**
 
 
 ```
 /**
     El siguiente provee el punto de entrada para google play services
     */
    protected GoogleApiClient mGoogleApiClient;
    /**
     * Representa una localizacion geografica.
     */
    protected Location mLastLocation;
 ```
 
 Al final de tu clase vas a implementar el siguiente método, el cual sirve para activas la geolocalización por medio de la API 
 que obtuviste de la consola de google, el cual se activa como un servicio cada vez que tu dispositivo se vaya a conectar.
 
 ```
 public synchronized  void buildGoogleApiClient(){
        mGoogleApiClient=new GoogleApiClient.Builder(this)
                .addConnectionCallbacks(this)
                .addOnConnectionFailedListener(this)
                .addApi(LocationServices.API)
                .build();

    }
 ```
A continuacion vas a implementar los siguientes métodos
```
@Override
    protected void onStart() {
        super.onStart();
        mGoogleApiClient.connect();
    }

    @Override
    protected void onStop() {
        super.onStop();
        if (mGoogleApiClient.isConnected()) {
            mGoogleApiClient.disconnect();
        }
    }
```

Ya con esto tienes las plantillas d elos principales métodos ahora los vas a rellenar con el siguiente código

Al final de tu método **onCreate** vas a invocar el método siguiente.
```
buildGoogleApiClient();
```


Listo eso es todo!!.
