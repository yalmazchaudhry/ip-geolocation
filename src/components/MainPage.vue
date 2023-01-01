<template>
  <v-container>
    <v-row class="d-flex justify-center">
      <v-col class="col-md-6">
        
       <div class="d-flex"> <v-text-field
            v-model="ip"
            label="Your IP"
            solo-inverted
            @change="getGeolocation(ip)"
          ></v-text-field><v-btn
              color="primary"
              dark
              :loading="loading"
              :disabled="loading"
                    class="ml-2 mt-2"
              
              @click="getGeolocation(ip)"
            >
              Ip Lookup
            </v-btn></div>
            <div class="d-flex justify-center" v-if="err==true"> 
          <v-alert
    text
    dismissible
    type="error"
    max-width=200
    
  >Invalid URL</v-alert></div>
        <v-simple-table v-if="showTable">
    
          <tr>
          <th class="text-left">
            Continent
          </th>
          <td>{{ ipData.continent }}</td>
          </tr>
        <tr>
          <th class="text-left">
            City
          </th>
          <td>{{ ipData.city }}</td>
          </tr>
          <tr>
          <th class="text-left">
            District
          </th>
          <td>{{ ipData.district }}</td>
          </tr>
        <tr>
          <th class="text-left">
            Country
          </th>
          <td>{{ipData.country}}</td>
          </tr>
          <tr>
          <th class="text-left">
            Country Code
          </th>
          <td>{{ ipData.countryCode }}</td>
        </tr>
        <tr>
          <th class="text-left">
            ISP
          </th>
          <td>{{ ipData.isp }}</td>
        </tr>
        <tr>
          <th class="text-left">
            Latitude
          </th>
          <td>{{ ipData.lat }}</td>
        </tr><tr>
          <th class="text-left">
            Longitude
          </th>
          <td>{{ ipData.lon }}</td>
        </tr>
        <tr>
          <th class="text-left">
            Origin
          </th>
          <td>{{ ipData.org }}</td>
        </tr>
        <tr>
          <th class="text-left">
            Region
          </th>
          <td>{{ ipData.region }}</td>
        </tr>
        <tr>
          <th class="text-left">
            Region Name
          </th>
          <td>{{ ipData.regionName }}</td>
        </tr>
        <tr>
          <th class="text-left">
            Time Zone
          </th>
          <td>{{ ipData.timezone }}</td>
        </tr>
        <tr>
          <th class="text-left">
            ZIP
          </th>
          <td>{{ ipData.zip }}</td>
        </tr>
        
  
  </v-simple-table>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    name: 'MainPage',
data(){
  return{
    ip:'',
    err:false,
    loading:false,
    ipData:{},
    showTable:false,
    clientIP:''
  }
},
created(){

  fetch('https://api.ipify.org?format=json')
  .then((response) => response.json())
  .then((data) => {
this.clientIP=data.ip
this.getGeolocation(data.ip)
          console.log(data)
        });
        
      
},
    
    methods:{
      getGeolocation(ip){
        if (
          /\b(?!(10)|192\.168|172\.(2[0-9]|1[6-9]|3[0-1])|(25[6-9]|2[6-9][0-9]|[3-9][0-9][0-9]|99[1-9]))[0-9]{1,3}\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)/g.test(
          ip
        )
      ){
        this.loading = true;
      } else {
        this.loading = false;
      }
        
        fetch(`http://ip-api.com/json/${ip}?fields=status,message,continent,country,countryCode,region,regionName,city,district,zip,lat,lon,timezone,isp,org,as,query`)
     .then((response) => response.json())
        .then((data) => {
          if(data){
          this.loading=false
        this.showTable=true}
          if(data.message=="invalid query"){
            this.err=true
            this.showTable=false
          }
          this.ipData=data;
          console.log(data);

        });

      }
    
    }

  }
</script>
