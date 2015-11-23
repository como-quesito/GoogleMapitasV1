# GoogleMapitasV1 
Este es un proyecto de geolocalización extremadamente básico. El primer paso es implementra las intrefaces siguientes a tu proyecto de plantilla de
de google maps:

´´´
//Implementra las siguientes dos interfaces
        GoogleApiClient.ConnectionCallbacks,
        GoogleApiClient.OnConnectionFailedListener {
´´´
 Al  hacer lo anterior te pedira implementar los métodos abstractos, implementalos, al final de tu **MainActivity** verás los siguientes métodos.
 
´´´
  @Override
    public void onConnected(Bundle bundle) {
        
    }

    @Override
    public void onConnectionSuspended(int i) {

    }

    @Override
    public void onConnectionFailed(ConnectionResult connectionResult) {

    }
 ´´´
 
 Posteriormente vas a declarar los siguientes dos atributos a tu **MainActivity**
 
 
 ´´´
 /**
     El siguiente provee el punto de entrada para google play services
     */
    protected GoogleApiClient mGoogleApiClient;
    /**
     * Representa una localizacion geografica.
     */
    protected Location mLastLocation;
 ´´´
 Al final de tu clase vas a implementar el siguiente método, el cual sirve para activas la geolocalización por medio de la API 
 que obtuviste de la consola de google, el cual se activa como un servicio cada vez que tu dispositivo se vaya a conectar.
 
 ´´´
 public synchronized  void buildGoogleApiClient(){
        mGoogleApiClient=new GoogleApiClient.Builder(this)
                .addConnectionCallbacks(this)
                .addOnConnectionFailedListener(this)
                .addApi(LocationServices.API)
                .build();

    }
 ´´´
