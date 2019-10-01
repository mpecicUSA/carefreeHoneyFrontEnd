<template>
    <v-container>
            <h3 className=''>Edit Product: {{ pullProductForEdit.title}}</h3>
            <v-form
            ref="form"
            >
            <v-text-field
            label="Title"
            v-model="title1"
            ></v-text-field>
            <v-text-field
            v-model="size1"
            label="Size"
            ></v-text-field>
            <v-text-field
            v-model="details1"
            label="Details"
            ></v-text-field>
            <v-text-field
            v-model="quantity1"
            label="Quantity"
            ></v-text-field>
            <v-checkbox
            v-model="onSale1"
            label="On Sale"
            ></v-checkbox>
            <v-checkbox
            v-model="freeShipping1"
            label="Free Shipping"
            ></v-checkbox>
            <v-text-field
            v-model="imgUrl1"
            label="Image URL"
            ></v-text-field>
            <v-text-field
            v-model="price1"
            label="Price"
            ></v-text-field>
            <v-btn 
            color="success"
            @click="submit"
            >
            Submit
            </v-btn>
            </v-form>
            <v-btn 
            color="red"
            @click="del"
            >
            Delete this Product from inventory
            </v-btn>
    </v-container>
</template>

<script>
import axios from "axios"
export default {
    data(){
    const { title, size, details, quantity, onSale, price, freeShipping, imgUrl, id} = this.$store.getters.getSpecificProduct
        return {
            title1: title,
            size1: size ,
            details1: details,
            quantity1: quantity,
            onSale1: onSale, 
            price1: price,
            freeShipping1: freeShipping, 
            imgUrl1: imgUrl,
            id1: id
        }
    },
    methods: { 
        submit: function(){
                console.log("button clicked")
                axios.post(`http://localhost:8000/products/edit/${this.id1}`, {
                    title: this.title1,
                    size: this.size1, 
                    details: this.details1,
                    quantity: this.quantity1, 
                    onSale: this.onSale1,
                    price: this.price1,
                    freeShipping: this.freeShipping1,
                    imgUrl: this.imgUrl1
                })
                .then((res)=> {
                    console.log(res)
                })
                .catch((err) => console.log(err));
                this.$router.push('/')
        },
        del: function(){
            axios.delete(`http://localhost:8000/products/delete/${this.id1}`)
            .then((res)=> {
                console.log(res)
            })
            .catch((err)=> {
                console.log(err)
            });
            this.$router.push('/')
        }
    },
    computed: {
        pullProductForEdit () {
            return this.$store.getters.getSpecificProduct
        }
    }
}
</script>

<style>

</style>