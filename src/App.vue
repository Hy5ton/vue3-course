<template>
    <div class="app">
        <nav class="navbar">
            <ul class="navbar-loc">
                <li class="mintify--btns"><a class="mintify--btns--styles">Mintify</a></li>
                <li class="first--top--btns"><a class="top--btns--styles">Dashboard</a></li>
                <li class="top--btns"><a class="top--btns--styles">About Us</a></li>
                <li class="top--btns"><a class="top--btns--styles">FAQ</a></li>
                <my-input
                class="searchLine"
                v-model="searchQuery"
                placeholder="🔍Search artwork"
                />
                <img class="image--navbar" src="../src/components/imageNavbar/email.png"/>
                <img class="image--navbar" src="../src/components/imageNavbar/moneybag.png"/>
            </ul>
        </nav>
        <div class="sidenav">
            <a href="#">Status</a>
            <a href="#">Price</a>
            <a href="#">Collection</a>
            <a href="#">Chains</a>
            <a href="#">Categories</a>
            <a href="#">Sale</a>
        </div>
        <h1 class="textLabel">Cryptographics</h1>
        <div class="app__btns">
            <my-button
            class="create__btn"
            @click="showDialog"
            >
                Create new item
            </my-button>
            <my-select class="sort--style"
                v-model="selectedSort"
                :options="sortOptions"
            />
        </div>
        <my-dialog v-model:show="dialogVisible">
            <post-form
            @create="createPost"
            />
        </my-dialog>
        <div>
            <post-list class="elements"
                :posts="sortedAndSearchedPosts"
                @remove="removePost"
            />
        </div>
    </div>
</template>

<script>
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyButton from "@/components/UI/MyButton.vue";
import MySelect from "@/components/UI/MySelect.vue";

export default{
    components: {
        MySelect,
        MyButton,
        PostForm, PostList
    },
    data() {
        return{
            posts: [
                {id: 1, title: 'The Holy Grail', body: 'Pixart Motion', type: 'Fixed price', price: '0.001 ETH', src:"imageList/1.png"},
                {id: 2, title: 'Mirror Glass Efect', body: 'Pixart Motion', type: 'Open bidding', price: '0.005 ETH', src:"imageList/2.png"},
                {id: 3, title: 'Neon in Life', body: 'Pixart Motion', type: 'Fixed price', price: '0.002 ETH', src:"imageList/3.png"},
                {id: 4, title: 'Oil Source', body: 'Pixart Motion', type: 'Fixed price', price: '0.001 ETH', src:"imageList/4.png"},
                {id: 5, title: 'World Surface', body: 'Pixart Motion', type: 'Open bidding', price: '0.004 ETH', src:"imageList/5.png"},
                {id: 6, title: 'Infinity Door', body: 'Pixart Motion', type: 'Fixed price', price: '0.005 ETH', src:"imageList/6.png"},
                {id: 7, title: 'Bi-conditional Effect', body: 'Pixart Motion', type: 'Fixed price', price: '0.002 ETH', src:"imageList/7.png"},
                {id: 8, title: 'Motion view', body: 'Pixart Motion', type: 'Open bidding', price: '0.009 ETH', src:"imageList/8.png"}
            ],
            dialogVisible: false,
            modificatorValue: '',
            selectedSort: '',
            searchQuery: '',
            sortOptions: [
                {value: 'title', name: 'Name' },
                {value: 'body', name: 'Description' },
                {value: 'type', name: 'Type' },
                {value: 'price', name: 'Price'}
            ]
        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
    },
    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
        },
        sortedAndSearchedPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    }
}

</script>

<style>
* {
    background: rgb(62, 72, 83);
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app{
    margin: 0;
    padding: 0;
}
.app__btns{
    display: flex;
    justify-content: right;
    margin: 50px 1480px;
    height: 150px;
    width: 350px;
}
.sort--style{
    font-size: 20px;
}
.create__btn{
    padding: 10px 15px;
    border-radius: 15px;
    color: black;
    border: 1px solid gray;
    background: rgb(101, 189, 101);
    margin-top: 80px;
    font-size:20px;
    font-weight: 700;
    font-family: Georgia, 'Times New Roman', Times, serif;
}
.textLabel{
    position: absolute; 
    font-size: 50px;
    top: 130px; 
    left: 300px; 
    color: white;
}
.searchLine{
    position: relative;
    max-width: 420px;
    background: #2e3741;
    color: white;
    left: 350px;
    border-radius: 10px;
    top: -25px;
}
.image--navbar{
    background: #2e3741;
    position: relative;
    color: white;
    left: 450px;
    top: -10px;
    height: 40px; 
    width: 40px; 
    margin-right: 20px;
}
.navbar{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 9999;
    border-style: solid;
    border-width: 1px;
    border-color: gray;
    margin: 0;
    color: #2e3741;
    background-color: #2e3741;
}
.navbar-loc{
    list-style: none; 
    margin: 0; 
    padding-left: 0; 
    margin-top:25px; 
    color: #2e3741;
    background-color: #2e3741;
}
.first--top--btns{
    float:left; 
    margin-right:40px; 
    padding-left: 160px;
    background-color: #2e3741;
}
.first--top--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 30px;
    text-decoration:none; 
    display: inline-block; 
    color:white;
    background-color: #2e3741;
}
.top--btns{
    float:left; 
    margin-right:40px; 
    background-color: #2e3741;
}
.mintify--btns{
    float:left; 
    margin-right:40px; 
    background-color: #2e3741;
}
.mintify--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 15px;
    text-decoration:none; 
    display: inline-block; 
    color:rgb(101, 189, 101);
    background-color: #2e3741;
}
.top--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 30px;
    text-decoration:none; 
    display: inline-block; 
    color:white;
    background-color: #2e3741;
}
.top--btns--styles:after {
    display: block; 
    content: ""; 
    height: 3px; 
    width: 0%; 
    color:rgb(101, 189, 101);
    background-color: rgb(101, 189, 101); 
}
.top--btns--styles:hover{
    color:rgb(101, 189, 101);
}
.top--btns--styles:hover:after,
.top--btns--styles:focus:after {
    width: 80%;
}
.sidenav {
    border-style: solid;
    border-width: 1px;
    border-color: gray;
    border-top: #2e3741;
    height: 100%; 
    width: 260px; 
    position: fixed; 
    z-index: 1;
    left: 0;
    background-color: #2e3741; 
    overflow-x: hidden; 
    padding-top: 72px;
}
.sidenav a {
    padding: 6px 8px 6px 16px;
    width: 220px;
    text-decoration: none;
    font-size: 20px;
    color: white;
    background-color: #2e3741;
    display: block;
    border-style: solid;
    border-width: 1px;
    border-color: gray;
    border-top: #2e3741;
    border-left: #2e3741;
    border-right: #2e3741;
}
.sidenav a:hover {
    color: rgb(101, 189, 101);
}
.main {
    margin-left: 160px; 
    padding: 0px 10px;
}
@media screen and (max-height: 450px) {
    .sidenav {padding-top: 15px;}
    .sidenav a {font-size: 18px;}
}
.elements{
    font-size:20px;
    color:white;
    border-radius: 15px;
    background: #4e565f;
    margin: 50px 290px;
    margin-top: 120px;
    width: 1545px;
}
</style>