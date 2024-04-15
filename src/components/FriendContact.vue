<template>
    <li>
        <h2>{{name}}   {{isFavorite  ? '(Favorite)' : ""}} </h2>
        <button @click="toggleDetails" > {{detailsAreVisible ? 'Hide' : 'Show'}}  Details</button>
        <button @click="toggleFavorite" > Favorite</button>

        <ul v-if="detailsAreVisible">
            <li><strong>Phone: </strong> {{phoneNumber}} </li>
            <li><strong>Email: </strong> {{emailAdress}} </li>
        </ul>
        <button @click="deleteFriend">Delete</button>
    </li>
</template>

<script>

//prop atarken kebap case yani phone-number  burada prop geçerken camel case yani phoneeNumber
    export default{
        //props:["name","phoneNumber","emailAdress","isFavorite"],
        //props:{
        //    name:String,
        //    phoneNumber:String,
        //    emailAdress:String,
        //    isFavorite:String
        //},
        props:{
            friendId:{
                type:String,
                required:true
            },
            name:{
                type:String,
                required:true
            },
            phoneNumber:{
                type:String,
                required:true
            },
            emailAdress:{
                type:String,
                required:true
            },
            isFavorite:{
                type:Boolean,
                required:false,
                
            }
        },
        //emits ler child to parent iletişiminde göndermiş olduğumuz fonksiyon adıdır Bunu kullanmasan da olur hata almazsın ama ne yaptığına dair yardımcı olur sana
        emits:["toggle-favorite"],

        //emits:{
        //    "toggle-favorite" : function(friendId){
        //        if(friendId){
        //            return true
        //        }
        //        else{
        //            return false
        //        }
        //    }
        //},

        //proplar bu şekillerde belirtilebilir
        //en aşağıda olan bir grup ile çalışırken herkes anlasın diye mantıklı
        //çünkü herhangi bir şey unutulduğunda direkt console da belirtiyor 
         data(){
            return{
                detailsAreVisible : false,
               
        }
    },
    methods:{
        toggleDetails(){
            this.detailsAreVisible = !this.detailsAreVisible
            },
        toggleFavorite(){
                this.$emit("toggle-favorite",this.friendId)
            },
        deleteFriend(){
            this.$emit("delete",this.friendId)
        }
        }
    }

// gelen propu method içinde değiştirmek vue da mutation hatasına sebep oluyor 
//bunu engellemek için ne yaptık 
//data içinde friendİsFavorite oluşturduk ve gelen prop değerlerini buraya atadık daha sonra bunu değişikliğe uğrattık
//Tek yönlü akış yöntemi olduğu için

</script>
