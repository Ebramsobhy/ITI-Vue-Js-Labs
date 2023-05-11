<template>
    <div class="container" id="mainApp">
        <div class="row">
            <div class="bg-black text-light d-flex justify-content-between align-items-baseLine fixed-top mb-3 p-3 fs-4">
                <a href="#" style="text-decoration: none;color:gold" @click.prevent="hideCart">Books</a>
                <div>
                    <small class="text-grey">{{wishList.books.length}} <span v-if="wishList.books.length == 1">item</span> <span v-else>items</span> with total price {{formatter(calcTotalPrice())}}</small>&nbsp;&nbsp;
                    <button class="btn btn-info" @click="showCart">Go To Wish List</button>
                </div>
            </div>
        </div>
        <!-- End Of Top Nav -->

        <div class="row" v-if="isBooksShown">
            <div  class="col-sm-12 col-md-6 col-lg-4" v-for="book in books" :key="book.id" :title="book.author"> 
                <div class="card my-3 hover-shadow">
                    <img class="card-img-top" :src="book.image" alt="Title">
                    <div class="card-body">
                        <h4 class="card-title">{{book.title}}</h4>
                        <hr>
                        <div class="d-flex justify-content-between align-baseline m-auto p-2">
                            <div class="left">
                                <h5>{{book.id}}</h5>
                                <h5 :class="book.pages > 50? 'more':'less'">{{book.pages}}</h5>
                                <h5>{{book.category}}</h5>
                            </div>
                            <div class="right">
                                <h5>{{book.author}}</h5>
                                <h5>{{formatter(book.price)}}</h5>
                                <button :class="checkAdded(book)? 'btn btn-secondary':'btn btn-primary'" :disabled="checkAdded(book)" @click="addToWishList(book)">Add To Check List</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- End Of Books -->

        <div class="row" v-if="isWishListShown">
            <div v-if="isWishListShown" class="m-auto text-center fs-4" style="margin-top: 90px !important;">
                <p v-if="wishList.books.length == 0" class="text-danger">Wish List is Empty &nbsp;&nbsp; <button @click="hideCart" type="button" class="btn btn-outline-info">Return To Books</button></p>
            </div>
            <table class="table">
                <thead>
                  <tr>
                    <th>ISBN</th>
                    <th>Title</th>
                    <th>Author</th>
                    <th>Pages</th>
                    <th>Category</th>
                    <th>Price</th>
                    <th>Actions</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="book in wishList.books" :key="book.id">
                    <td>{{ book.id }}</td>
                    <td>{{ book.title }}</td>
                    <td>{{ book.author }}</td>
                    <td :class="book.pages > 50 ? 'more' : 'less'">{{ book.pages }}</td>
                    <td>{{ book.category }}</td>
                    <td>{{ formatter(book.price) }}</td>
                    <td><button class="btn btn-danger" @click="removeFromWishList(book)">Remove From Check List</button></td>
                  </tr>
                </tbody>
              </table>
        </div>
        <!-- End Of Books WishList -->
    </div>
</template>

<script>
    import {books} from '../data'
    
    export default{
        data() {
            return {
                books,
                isWishListShown: false,
                isBooksShown: true,
                wishList:{
                    books: []
                }
            }
        },
        methods: {
            formatter(input){
                const formatter = new Intl.NumberFormat('ar-SA', {
                style: 'currency',
                currency: 'SAR',
                });

                return formatter.format(input);
            },
            showCart(){
                this.isWishListShown = true;
                this.isBooksShown = false;
            },
            hideCart(){
                this.isWishListShown = false;
                this.isBooksShown = true;
            },
            checkAdded(book){
                return this.wishList.books.some( (currentBook)=>(book === currentBook)  );
            },
            addToWishList(book){
                this.wishList.books.push(book);                    
            },
            removeFromWishList(book){
                let index = this.wishList.books.indexOf(book);
                if( index !== -1 ){
                    this.wishList.books.splice(index,1);
                }
            },
            calcTotalPrice(){
                let total = 0; 
                for(let book in this.wishList.books){
                    total += this.wishList.books[book].price;
                }
                return total;
            }
        },  
    }
</script>

<style scoped>
    .more{
        color: green;
    }
    .less{
        color: orange;
    }
    .none{
        color: red;
    }

    .card:hover{
        cursor: pointer;
        box-shadow: 5px 10px 18px #888888;
    }
</style>