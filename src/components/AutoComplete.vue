<template>
    <div>
        <h2>Type Your Address</h2>
        <vue-google-autocomplete
            ref="address"
            id="map"
            classname="form-control"
            placeholder="Please type your address"
            v-on:placechanged="getAddressData"
            types=""
        >
        </vue-google-autocomplete>
        <br>
        <button @click="resetInput" class="reset-btn">Reset</button>
        <ul v-if="address" class="address">
        <li>Administrative area level 1 : <strong>{{address.administrative_area_level_1}}</strong></li>
        <li>Administrative area level 2 : <strong>{{address.administrative_area_level_2}}</strong></li>
        <li>Country :<strong>{{address.country}}</strong></li>
        <li>Latitude :<strong>{{address.latitude}}</strong></li>
        <li>Longitude :<strong>{{address.longitude}}</strong></li>
        <li>Locality :<strong>{{address.locality}}</strong></li>
        </ul>
        
    </div>
</template>

<script>
    import VueGoogleAutocomplete from 'vue-google-autocomplete'

    export default {
        name:'AutoComplete',
        components: { VueGoogleAutocomplete },

        data: function () {
            return {
              address: ''
            }
        },

        mounted() {
            // To demonstrate functionality of exposed component functions
            // Here we make focus on the user input
            this.$refs.address.focus();
        },

        methods: {
            /**
            * When the location found
            * @param {Object} addressData Data of the found location
            * @param {Object} placeResultData PlaceResult object
            * @param {String} id Input container ID
            */
            getAddressData(addressData, placeResultData, id) {
                this.address = addressData;
            },
            resetInput(){
                this.address = '';
                this.$refs.address.clear();
            }
        }
    }
</script>
<style scoped>
    .address{
        max-width:500px;
        margin:20px auto;
    }
    .address li{
        list-style: none;
    }
    input[type="text"]#map{
        width:60%;
        height:32px;
        padding:4px;
        border:1px solid #ddd;
        border-radius:4px;
        font-size:18px;
    }
    input[type="text"]#map:focus{
        box-shadow:none;
        outline:none;
        border:1px solid #999;
    }
    .reset-btn{
        margin-top:10px;
        color:#fff;
        padding:10px 30px;
        border-radius:4px;
        box-shadow:0 1px 10px rgba(52, 128, 241, 0.52);
        background:rgb(43, 133, 236);
    }
</style>
