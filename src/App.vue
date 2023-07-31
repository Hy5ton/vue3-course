<template>
    <div class="app">
        <nav class="navbar">
            <ul class="navbar-loc">
                <img class="mintify--image" src="../src/components/imageNavbar/list.svg"/>
                <li class="mintify--btns"><a class="mintify--btns--styles">Mintify</a></li>
                <li class="first--top--btns"><a class="top--btns--styles">Dashboard</a></li>
                <li class="top--btns"><a class="top--btns--styles">About Us</a></li>
                <li class="top--btns"><a class="top--btns--styles">FAQ</a></li>
                <my-input
                class="material-symbols-outlined"
                v-model="searchQuery"
                placeholder='Search'
                />
                <div class="border-navbar"><img class="image--navbar" src="../src/components/imageNavbar/email.svg"/></div>
                <div class="border-navbar"><img class="image--navbar" src="../src/components/imageNavbar/sqrt.svg"/></div>
                <div class="border-navbar"><img class="image--navbar" src="../src/components/imageNavbar/moneybag.svg"/></div>
                <img class="user--navbar" src="../src/components/imageNavbar/bg.png"/>
                <a class="username--navbar">Leslie Alexandre</a> 
            </ul>
        </nav>
        <div class="sidenav">
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Status</a>
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Price</a>
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Collection</a>
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Chains</a>
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Categories</a>
            <img class="image--arrow-sidebar" src="../src/components/imageNavbar/arrow.svg"/>
            <a class="sidenav-btns">Sale</a>
        </div>
        <h1 class="textLabel">Cryptographics</h1>
        <div class="app__btns">
            <button
            class="create__btn"
            @click="showDialog"
            >
                Create new item
            </button>
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
            />
        </div>
    </div>
</template>

<script>
// @remove="removePost" под :posts - кнопка удаления айтема
import PostForm from "@/components/PostForm.vue";
import PostList from "@/components/PostList.vue";
import MyButton from "@/components/UI/MyButton.vue";
import MySelect from "@/components/UI/MySelect.vue";
import ItemDialog from "@/components/UI/ItemDialog.vue";

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
    background: #2B2C33;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
.material-symbols-outlined {
    font-size: 20px;
    position: relative;
    padding-left: 25px;
    max-width: 420px;
    color: white;
    left: 190px;
    border-radius: 10px;
    top: -20px;
    font-variation-settings:
    'FILL' 0,
    'wght' 100,
    'GRAD' 0,
    'opsz' 48
}
.app{
    font-family: Oswald;
    font-style: normal;
    font-weight: 900;
    line-height: normal;
    margin: 0;
    padding: 0;
}
.app__btns{
    cursor: pointer;
    margin: 50px 1480px;
    height: 150px;
    width: 350px;
}
.sort--style{
    font-size: 20px;
}
.create__btn{
    cursor: pointer;
    position: relative;
    padding: 10px 15px;
    border-radius: 15px;
    top: 70px;
    left: 175px;
    display: flex;
    align-items: center;
    color: black;
    border: 1px solid #383940;
    background: var(--green, #38F2AF);
    font-size:25px;
    font-weight: 500;
    font-family: Oswald;
}
.textLabel{
    position: absolute; 
    font-size: 32px;
    top: 130px; 
    left: 300px; 
    color: white;
}
.searchLine{
    position: relative;
    font-family: Oswald;
    padding-left: 25px;
    max-width: 420px;
    color: white;
    left: 190px;
    border-radius: 10px;
    top: -20px;
}

.image--navbar{
    cursor: pointer;
    width: 22px;
    background: #373943;
    border-radius: 25px;
    left: 9px;
    top: 9px;
    position: relative;
    color: white;
    margin-right: 20px;
}
.border-navbar{
    cursor: pointer;
    margin-right: 20px;
    border-radius: 25px;
    background: #373943;
    display:inline-block;
    position: relative;
    left: 330px;
    top: -25px;
    height: 40px; 
    width: 40px; 
}
.user--navbar{
    cursor: pointer;
    height: 40px; 
    width: 40px;
    left: 360px;
    top: -7px;
    background: #373943;
    border-radius: 25px;
    position: relative;
    color: white;
    margin-right: 20px;
}
.username--navbar{
    cursor: pointer;
    font-family: Oswald;
    font-size: 22px;
    background: #25272E;
    position: relative;
    color: white;
    left: 370px;
    top: -20px;
    height: 40px; 
    width: 100px; 
    margin-right: 20px;
}
.navbar{
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 5;
    border-style: solid;
    border-width: 1px;
    border-color: #383940;
    margin: 0;
    color: #25272E;
    background-color: #25272E;
    flex-wrap: nowrap;
}
.navbar-loc{
    list-style: none; 
    margin: 0; 
    padding-left: 0; 
    margin-top:25px; 
    color: #25272E;
    background-color: #25272E;
}
.first--top--btns{
    cursor: pointer;
    float:left; 
    margin-right:40px; 
    padding-left: 140px;
    background-color: #25272E;
}
.first--top--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 30px;
    text-decoration:none; 
    display: inline-block; 
    color:white;
    background-color: #25272E;
}
.top--btns{
    cursor: pointer;
    float:left; 
    margin-right:40px; 
    background-color: #25272E;
}
.mintify--btns{
    cursor: pointer;
    float:left; 
    margin-right:50px;
    padding-left: 25px; 
    background-color: #25272E;
}
.mintify--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 25px;
    text-decoration:none; 
    display: inline-block; 
    color:var(--green, #38F2AF);;
    background-color: #25272E;
}
.mintify--image{
    display: inline-block;
    position: absolute; 
    top: 35px; 
    left: 30px;  
}
.top--btns--styles{
    text-decoration: none;
    font-size: 20px;
    margin-left: 30px;
    text-decoration:none; 
    display: inline-block; 
    color:white;
    background-color: #25272E;
}
.top--btns--styles:after {
    display: block; 
    content: ""; 
    height: 3px; 
    width: 0%; 
    color:var(--green, #38F2AF);
    background-color: var(--green, #38F2AF); 
}
.top--btns--styles:hover{
    color:var(--green, #38F2AF);
}
.top--btns--styles:hover:after,
.top--btns--styles:focus:after {
    width: 80%;
}
.sidenav {
    border-style: solid;
    border-width: 1px;
    border-color: #383940;
    border-top: #25272E;
    height: 100%; 
    width: 260px; 
    position: fixed; 
    z-index: 1;
    left: 0;
    background-color: #25272E; 
    overflow-x: hidden; 
    padding-top: 121px;
}
.sidenav a {
    cursor: pointer;
    top: -58px;
    padding: 6px 8px 10px 0px;
    width: 160px;
    text-decoration: none;
    font-size: 20px;
    color: white;
    background-color: #25272E;
    display: block;
    border-style: solid;
    border-width: 1px;
    border-color: #383940;
    border-top: #2e3741;
    border-left: #2e3741;
    border-right: #2e3741;
}
.sidenav a:hover {
    color: var(--green, #38F2AF);
}
.image--arrow-sidebar{
    cursor: pointer;
    background: #25272E;
    position: relative;
    left: 170px;
    top: -22px;
    z-index: 9999;
}
.main {
    margin-left: 160px; 
    padding: 0px 10px;
}
@media screen and (max-height: 450px) {
    .sidenav {padding-top: 15px;}
    .sidenav a {font-size: 18px;}
}
.sidenav-btns{
    position:relative;
    left: 30px;
}
.elements{
    font-size:20px;
    color:white;
    border-radius: 15px;
    background: #373943;
    margin: 50px 290px;
    margin-top: 120px;
    width: 1545px;
}
</style>