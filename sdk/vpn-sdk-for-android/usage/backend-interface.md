# Backend interface

### List available locations

```
sdk.getBackend().locations(ConnectionType.HYDRA_TCP, new Callback<AvailableLocations>() {
        @Override    
        public void success(@NonNull AvailableLocations availableLocations) {
           
        }    
        @Override    
        public void failure(@NonNull VpnException e) { 
        }
 });
```

### List available countries

```
sdk.getBackend().countries(ConnectionType.HYDRA_TCP, new Callback<AvailableCountries>() {
    @Override
    public void success(AvailableCountries response) {
        
    }

    @Override
    public void failure(HydraException error) {
        
    }
});
```



### Purchases functionality

```
sdk.getBackend().purchase("json from google", new CompletableCallback() {
   @Override
   public void complete() {
       //purchase request success
   }

   @Override
   public void error(VpnException e) {
        //failed to process purchase
   }
});
sdk.getBackend().deletePurchase(purchaseID, new CompletableCallback() {
   @Override
   public void complete() {
       //request success
   }

   @Override
   public void error(VpnException e) {
        //failed to process request
   }
});
```

### Get data about user

```
//get information about remaining traffic for user
sdk.getBackend().remainingTraffic(new Callback<RemainingTraffic>() {
    @Override
    public void success(@NonNull RemainingTraffic remainingTraffic) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
//get information about current logged in user
sdk.getBackend().currentUser(new Callback<User>() {
    @Override
    public void success(@NonNull User user) {
        
    }

    @Override
    public void failure(@NonNull VpnException e) {

    }
});
```

###
