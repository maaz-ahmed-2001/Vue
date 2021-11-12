<template>
  <div>
    <div id="container">
    <div id="form">
        <h3>Filter</h3>
        <div>
        <span>Sort By</span><br />
        <label>
        <input
          type="radio"
          id="price-sort"
          name="sorting"
          value="max"
          v-model="sortedType"
          v-on:click="max()"
            />Max - Min Price</label>
        <label>
        <input
          type="radio"
          id="price-sort"
          name="sorting"
          value="min"
          v-model="sortedType"
          v-on:click="min()"
            />Min - Max Price</label
      ><br />
      </div>
          <hr/>
        <div>
      
          
        <span>Packages</span><br />
        <label>
        <input
          type="radio"
          id="package"
          name="package"
          value="Spacespot Explorer"
          checked
          v-model="packages"
          
        />Spacespot Explorer</label><br />
        <label>
        <input
          type="radio"
          id="package"
          name="package"
          value="Chill Trip"
          

          v-model="packages" />Chill
        Trip </label
      ><br />
      </div>
      <hr/>
        <div>
      
        <span>Price</span> <span>{{ price }} $</span><br />
        <label>
        0$
        <input
          type="range"
          min="0"
          max="2000"
          id="cost"
          name="id"
          v-model="price"
          
        
        />
        2000$
        </label>
      
      <br />
      </div>
      <hr/>
      <div>
        <span>Destinations</span> <br />
      <div id="dest">
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Costa Rica"
            v-model="destination"
          />Costa Rica
        </label>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Greece"
            v-model="destination"
          />Greece
        </label>
        <br/>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Peru"
            v-model="destination"
          />Peru
        </label>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Sydney"
            v-model="destination"
          />Sydney
        </label>
        <br/>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Montreal"
            v-model="destination"
          />Montreal
        </label>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Bora Bora"
            v-model="destination"
          />Bora Bora
        </label>
        <br/>
        <label>
          <input
            type="checkbox"
            id="destination"
            name="destination"
            value="Auckland"
            v-model="destination"
          />Auckland
        </label>
      </div>
      <div id="btn-div">
      <button v-on:click="getTrips()" >Search</button>
      </div>
      </div>
    </div>
    <div id="trips">
        <div v-for="item in product" :key="item" class="cards">
            <img v-bind:src="item.pic"/>
            <div class="card-info">
                <h3 >{{item.city}} {{item.country}}</h3>
                <p >${{item.cost}}.00</p>
                <h4 >Destination description</h4>
                <p >{{item.description}}</p>
                <button>Reserve trip</button>
        
            </div>
            
        </div>
        
    </div>
    
    </div>
  </div>
</template>

<script>

export default {
  name: "Form",
  methods:{
    getTrips(){
        this.product=[]
        for(let i = 0 ; i < this.data.length ; i++){
            if(this.price >= this.data[i].cost && this.packages == this.data[i].package.package_name){     
                if(this.destination.length !== 0  ){
                    for(let j = 0 ; j < this.destination.length ; j++){
                        if(this.destination[j] === this.data[i].location.city){
                            console.log("****hello******")
                            this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                            console.log(this.product,this.destination[j],this.data[i].location.city)
                        }
                        
                        else{
                            console.log("Dest not found",this.destination)
                        }
                    }
                }
                else{
                    this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                    console.log(this.product,this.destination)
                }
            }
        }
        console.log("outside main FOR")
        if(this.sortedType === "min"){
            this.product.sort((a,b)=> a.cost-b.cost)
            console.log(this.product)
        }
        if(this.sortedType === "max"){
            this.product.sort((a,b)=> b.cost-a.cost)
            console.log(this.product)
        }   
    },
    max(){
        this.product.sort((a,b)=> b.cost-a.cost)
    },
    min(){
        this.product.sort((a,b)=> a.cost-b.cost)
    },
    
      
  },
    watch:{
        destination: function(){
             this.product=[]
        for(let i = 0 ; i < this.data.length ; i++){
            if(this.price >= this.data[i].cost && this.packages == this.data[i].package.package_name){     
                if(this.destination.length !== 0  ){
                    for(let j = 0 ; j < this.destination.length ; j++){
                        if(this.destination[j] === this.data[i].location.city){
                            console.log("****hello******")
                            this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                            console.log(this.product,this.destination[j],this.data[i].location.city)
                        }
                        
                        else{
                            console.log("Dest not found",this.destination)
                        }
                    }
                }
                else{
                    this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                    console.log(this.product,this.destination)
                }
            }
        }
        console.log("outside main FOR")
        if(this.sortedType === "min"){
            this.product.sort((a,b)=> a.cost-b.cost)
            console.log(this.product)
        }
        if(this.sortedType === "max"){
            this.product.sort((a,b)=> b.cost-a.cost)
            console.log(this.product)
        }   
        },
        packages:function(){
             this.product=[]
        for(let i = 0 ; i < this.data.length ; i++){
            if(this.price >= this.data[i].cost && this.packages == this.data[i].package.package_name){     
                if(this.destination.length !== 0  ){
                    for(let j = 0 ; j < this.destination.length ; j++){
                        if(this.destination[j] === this.data[i].location.city){
                            console.log("****hello******")
                            this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                            console.log(this.product,this.destination[j],this.data[i].location.city)
                        }
                        
                        else{
                            console.log("Dest not found",this.destination)
                        }
                    }
                }
                else{
                    this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                    console.log(this.product,this.destination)
                }
            }
        }
        console.log("outside main FOR")
        if(this.sortedType === "min"){
            this.product.sort((a,b)=> a.cost-b.cost)
            console.log(this.product)
        }
        if(this.sortedType === "max"){
            this.product.sort((a,b)=> b.cost-a.cost)
            console.log(this.product)
        }
        },
        price:function(){
             this.product=[]
        for(let i = 0 ; i < this.data.length ; i++){
            if(this.price >= this.data[i].cost && this.packages == this.data[i].package.package_name){     
                if(this.destination.length !== 0  ){
                    for(let j = 0 ; j < this.destination.length ; j++){
                        if(this.destination[j] === this.data[i].location.city){
                            console.log("****hello******")
                            this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                            console.log(this.product,this.destination[j],this.data[i].location.city)
                        }
                        
                        else{
                            console.log("Dest not found",this.destination)
                        }
                    }
                }
                else{
                    this.product.push({city:this.data[i].location.city,cost:this.data[i].cost,trip:this.data[i].package.package_name,pic:"https://media.istockphoto.com/photos/mount-hood-oregon-picture-id1268487061?b=1&k=20&m=1268487061&s=170667a&w=0&h=3fHYwaImlqUETcjCnSV7YO2-PzCFvaX6VSQaiGfWqpc=",country:this.data[i].location.country,description:this.data[i].location.destination_description})
                    console.log(this.product,this.destination)
                }
            }
        }
        console.log("outside main FOR")
        if(this.sortedType === "min"){
            this.product.sort((a,b)=> a.cost-b.cost)
            console.log(this.product)
        }
        if(this.sortedType === "max"){
            this.product.sort((a,b)=> b.cost-a.cost)
            console.log(this.product)
        }
        }
    },
  
  data() {
    return {
      price: 1000,
      destination:[],
      packages:"Spacespot Explorer",
      product:[],
      sortedType:"ascending",

      data : [
    {
        "id": 1,
        "location": {
            "id": 1,
            "city": "Costa Rica",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 1,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=a4731c3667b520aaebd71f7317374c653707156c73e7b0fe6eb254916db38387",
                    "location": 1
                }
            ],
            "average_cost": [
                {
                    "location_id": 1,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 1,
            "package_name": "Chill Trip",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=1878640071f343586633c77955bd4ab0ca21e018ea46c48b1b736f4134cca472",
            "activities_allowed": 2
        },
        "activity": [
            {
                "id": 5,
                "activity": "Testing3",
                "image": "https://spacespot.s3.amazonaws.com/images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=7210fd68324ba30e734bae00fb063eb42898d959864aeb116dd6f6dcfee63a77",
                "category": "Testing Category"
            },
            {
                "id": 7,
                "activity": "Testing5",
                "image": "https://spacespot.s3.amazonaws.com/download_5bBPhWK.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=b80eb6f1a6863338c4970b4eb6a4610fce022dff7ffd3b040cd663c5aae40ebd",
                "category": "New Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 2,
        "location": {
            "id": 2,
            "city": "Bora Bora",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Test",
            "images": [
                {
                    "id": 2,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=7fe23f9e03ebf74df176a1f11aeb34f136a384c6e3a36d711fe285eaf15bebbf",
                    "location": 2
                },
                {
                    "id": 3,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_3_0KgQuIY.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=a058968f2f441473b6836e67ba9fc90f9262c78a545810a0a31a0f202d7a6950",
                    "location": 2
                }
            ],
            "average_cost": [
                {
                    "location_id": 2,
                    "avg_cost": 1400.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 4,
                "activity": "Testing2",
                "image": "https://spacespot.s3.amazonaws.com/download_1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=f7e8635c72aaa8dcd72d7d3b75a02000c2483a990f1fa430d74d0e958353b9ad",
                "category": "Testing Category"
            }
        ],
        "cost": 1900,
        "no_of_days": 0
    },
    {
        "id": 3,
        "location": {
            "id": 6,
            "city": "Montreal",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 7,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_7.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=4a39550a72d43f3898bda9b14847531b18664fa2f53c928e5c3bec2b50c095a8",
                    "location": 6
                }
            ],
            "average_cost": [
                {
                    "location_id": 6,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 6,
                "activity": "Testing4",
                "image": "https://spacespot.s3.amazonaws.com/photo-1551632811-561732d1e306_TQ2jruX.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=8461cfc8394aedbdd56c54736757484127700d9d3c702096c5e1586de66814ac",
                "category": "Testing Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 4,
        "location": {
            "id": 4,
            "city": "Sydney",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 5,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_5.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=f2454cd8d68cef88ebee412e74fc0a89d77a5248319d8f2399f47f7b11fd9ea7",
                    "location": 4
                }
            ],
            "average_cost": [
                {
                    "location_id": 4,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 1,
            "package_name": "Chill Trip",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=1878640071f343586633c77955bd4ab0ca21e018ea46c48b1b736f4134cca472",
            "activities_allowed": 2
        },
        "activity": [
            {
                "id": 6,
                "activity": "Testing4",
                "image": "https://spacespot.s3.amazonaws.com/photo-1551632811-561732d1e306_TQ2jruX.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=8461cfc8394aedbdd56c54736757484127700d9d3c702096c5e1586de66814ac",
                "category": "Testing Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 5,
        "location": {
            "id": 5,
            "city": "Auckland",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 6,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_6.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=c5693a8cd593337154f515af3391be1a7b381154b430719fe377a4ce786d136b",
                    "location": 5
                }
            ],
            "average_cost": [
                {
                    "location_id": 5,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 2,
                "activity": "Skating",
                "image": "https://spacespot.s3.amazonaws.com/gettyimages-885411578-612x612.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=cb65f848e09deebbdcf46d07dd41cc9331e16c36fa169e5f2e1276509109d9ba",
                "category": "Testing Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 6,
        "location": {
            "id": 7,
            "city": "Peru",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 8,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_8.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=abfdc0d9928b5fa300daeb3cdc63a3f58742a8fea38f18c876259b18b889ce2e",
                    "location": 7
                }
            ],
            "average_cost": [
                {
                    "location_id": 7,
                    "avg_cost": 1200.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 6,
                "activity": "Testing4",
                "image": "https://spacespot.s3.amazonaws.com/photo-1551632811-561732d1e306_TQ2jruX.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=8461cfc8394aedbdd56c54736757484127700d9d3c702096c5e1586de66814ac",
                "category": "Testing Category"
            }
        ],
        "cost": 1200,
        "no_of_days": 0
    },
    {
        "id": 7,
        "location": {
            "id": 3,
            "city": "Greece",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 4,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_4.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=813b11c01c1b3526158e47a788a340e0c72c34fd11c85f2168d419c4e9e4915b",
                    "location": 3
                }
            ],
            "average_cost": [
                {
                    "location_id": 3,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 5,
                "activity": "Testing3",
                "image": "https://spacespot.s3.amazonaws.com/images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=7210fd68324ba30e734bae00fb063eb42898d959864aeb116dd6f6dcfee63a77",
                "category": "Testing Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 8,
        "location": {
            "id": 1,
            "city": "Costa Rica",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Testing",
            "images": [
                {
                    "id": 1,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_2.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=a4731c3667b520aaebd71f7317374c653707156c73e7b0fe6eb254916db38387",
                    "location": 1
                }
            ],
            "average_cost": [
                {
                    "location_id": 1,
                    "avg_cost": 900.0
                }
            ]
        },
        "package": {
            "id": 2,
            "package_name": "Spacespot Explorer",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download_X7eBzor.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=341dd639df82994fc64dc933950c67045ad96225000efaa0955ed74ae8b2c39c",
            "activities_allowed": -1
        },
        "activity": [
            {
                "id": 4,
                "activity": "Testing2",
                "image": "https://spacespot.s3.amazonaws.com/download_1.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=f7e8635c72aaa8dcd72d7d3b75a02000c2483a990f1fa430d74d0e958353b9ad",
                "category": "Testing Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    },
    {
        "id": 9,
        "location": {
            "id": 2,
            "city": "Bora Bora",
            "country": "Testing",
            "best_sellers": true,
            "top_destination": true,
            "destination_description": "Test",
            "images": [
                {
                    "id": 2,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_3.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=7fe23f9e03ebf74df176a1f11aeb34f136a384c6e3a36d711fe285eaf15bebbf",
                    "location": 2
                },
                {
                    "id": 3,
                    "image": "https://spacespot.s3.amazonaws.com/media/destination_images/download_3_0KgQuIY.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=a058968f2f441473b6836e67ba9fc90f9262c78a545810a0a31a0f202d7a6950",
                    "location": 2
                }
            ],
            "average_cost": [
                {
                    "location_id": 2,
                    "avg_cost": 1400.0
                }
            ]
        },
        "package": {
            "id": 1,
            "package_name": "Chill Trip",
            "package_description": "Testing",
            "package_images": "https://spacespot.s3.amazonaws.com/media/package_images/download.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=1878640071f343586633c77955bd4ab0ca21e018ea46c48b1b736f4134cca472",
            "activities_allowed": 2
        },
        "activity": [
            {
                "id": 2,
                "activity": "Skating",
                "image": "https://spacespot.s3.amazonaws.com/gettyimages-885411578-612x612.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=cb65f848e09deebbdcf46d07dd41cc9331e16c36fa169e5f2e1276509109d9ba",
                "category": "Testing Category"
            },
            {
                "id": 3,
                "activity": "Testing1",
                "image": "https://spacespot.s3.amazonaws.com/download.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=638516265b854401cf823fb9f98bd0fd72db779fb6dcdfac76847ec735e3cb0c",
                "category": "Testing Category"
            },
            {
                "id": 5,
                "activity": "Testing3",
                "image": "https://spacespot.s3.amazonaws.com/images.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=7210fd68324ba30e734bae00fb063eb42898d959864aeb116dd6f6dcfee63a77",
                "category": "Testing Category"
            },
            {
                "id": 7,
                "activity": "Testing5",
                "image": "https://spacespot.s3.amazonaws.com/download_5bBPhWK.jpg?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIA4PF3GLASJ4OGSKVX%2F20211101%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20211101T173655Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=b80eb6f1a6863338c4970b4eb6a4610fce022dff7ffd3b040cd663c5aae40ebd",
                "category": "New Category"
            }
        ],
        "cost": 900,
        "no_of_days": 0
    }
]
    };
  },
  
};
</script>
<style scoped>
*{
    margin: 0;
    padding: 0;
    user-select: none;

}

#form{
    border: 1px solid rgb(221, 221, 221);
    border-radius: 15px;
    overflow: hidden;
    width: 35%;
    margin: 20px;
    display: flex;
    flex-direction: column;
    height: fit-content;
    /* justify-content: center; */
    /* align-items: center; */

}
#trips{
    width:60%;
    display: flex;

}
#container{
    display: flex;
    justify-content: center;
}
img{
    height: 30vh;
    min-width: 50%;
    max-width: 60%;
    border-radius: 20px;
}
.cards{
    display: flex;
    justify-content: space-between;
    width: fit-content;
    align-items: center;
    height: fit-content;
    padding: 5px;
    flex-direction: row;
    width: fit-content;
}
#form h3{
    background-color: rgb(252,164,100);
    color: #fff;
    padding: 5px 0px 5px 15px;
    font-weight: 300;
    font-size: 14px;
}
#form div{
    margin-top: 5px;
    padding: 10px;
}
hr{
    margin: 0px 5px 0px 5px ;
    background-color:rgb(194, 194, 194) ;
    height: 1px;
    border: none;
}
label{
    color:#999;
    margin: 5px;
    font-size: 14px;
}
#form button{
    background-color: rgb(252,164,100);
    color: #fff;
    border-radius: 15px;
    width: 100%;
    height: 30px;
    border: none;
}
#form button:hover{
    background-color: rgb(255, 148, 72);
}
#form input:hover{
   
    background-color: rgb(252,164,100);
    color: rgb(252,164,100);
}
.card-info{
    color: #444;
    margin: 5px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    height: 30vh;
    padding: 10px;
    width: fit-content;
}
.card-info p {
    color: rgb(252,164,100);
}
.card-info button{
    border: none;
    border-radius: 15px;
    height: 30px;
    width: 125px;
    background-color: rgb(252,164,100);
    color: #fff;
    font-size: 12px;
    font-weight: 800;
}
.card-info button:hover{
    background-color: rgb(255, 148, 72);
}
#btn-div{
    text-align: center;
}
span{
    font-size: 15px;
    color:#888;
    font-weight: 600;
}
#trips{
    position: relative;
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
    align-items: center;
    flex-wrap: wrap;
}
#dest{
    margin-top: -10px;
    margin-left: -10px;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    flex: 1 0 45%;
}
#dest label{
    width: 45%;
    
}
input{
    margin: 5px;
}
#form span{
    margin-left: 5px;
}

</style>