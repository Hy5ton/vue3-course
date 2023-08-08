<template>
    <div class="app">
        <nav class="navbar">
            <ul class="navbar-loc">
                <li class="mintify--btns"><img class="mintify--image" src="../src/components/imageNavbar/list.svg"/><a class="mintify--btns--styles">Mintify</a></li>
                <li class="first--top--btns"><a class="top--btns--styles">Dashboard</a></li>
                <li class="top--btns"><a class="top--btns--styles">About Us</a></li>
                <li class="top--btns"><a class="top--btns--styles">FAQ</a></li>
                <input
                class="material-symbols-outlined"
                v-model="searchQuery"
                placeholder='Search'
                />
                <div class="border-navbar"><img class="image--navbar" src="../src/components/imageNavbar/email.svg"/>
                <img class="image--navbar" src="../src/components/imageNavbar/sqrt.svg"/>
                <img class="image--navbar" src="../src/components/imageNavbar/moneybag.svg"/></div>
                <a class="username--navbar"><img class="user--navbar" src="../src/components/imageNavbar/bg.png"/>Leslie Alexandre</a> 
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
    height: 33px;
    font-size: 20px;
    max-width: 420px;
    color: white;
    /* left: 190px; */
    border-radius: 10px;
    border: 1px solid #383940;
    /* top: -20px; */
    font-variation-settings:
    'FILL' 0,
    'wght' 0,
    'GRAD' 0,
    'opsz' 0
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
    top: 150px;
}
.create__btn{
    cursor: pointer;
    position: relative;
    padding: 10px 15px;
    border-radius: 15px;
    top: 60px;
    left: 175px;
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
    color: white;
}
.searchLine{
    flex-shrink: 2;
    font-family: Oswald;
    max-width: 420px;
    color: white;
    border-radius: 10px;
}

.image--navbar{
    cursor: pointer;
    width: 30px;
    background: #373943;
    border-radius: 25px;
    position: relative;
    color: white;
}
.border-navbar{
    min-width: 100px;
    cursor: pointer;
    border-radius: 25px;
    background: #25272E;
    width: 30px; 
    height: 30px;
}
.user--navbar{
    height: 33px;
    cursor: pointer;
    background: #373943;
    border-radius: 25px;
    color: white;
    margin-right: 10px;
    align-items: center;
}
.username--navbar{
    display: flex;
    align-items: center;
    flex-shrink: 0;
    height: 33px;
    width: 200px;
    cursor: pointer;
    font-size: 22px;
    background: #25272E;
    color: white;
}
.navbar-loc{
    height: 90px;
    align-items: center;
    border-style: solid;
    border-width: 1px;
    border-color: #383940;
    display: flex;
    flex-wrap: no-wrap;
    justify-content: space-around;
    /* margin-top:25px;  */
    color: #25272E;
    background-color: #25272E;
}
.first--top--btns{
    cursor: pointer;
    float:left; 
    background-color: #25272E;
}
.first--top--btns--styles{
    text-decoration: none;
    font-size: 20px;
    text-decoration:none; 
    display: inline-block; 
    color:white;
    background-color: #25272E;
}
.top--btns{
    cursor: pointer;
    float:left; 
    background-color: #25272E;
}
.mintify--btns{
    cursor: pointer;
    background-color: #25272E;
}
.mintify--btns--styles{
    height: 33px;
    text-decoration: none;
    font-size: 20px;
    text-decoration:none; 
    display: inline-block; 
    color:var(--green, #38F2AF);;
    background-color: #25272E;
}
.mintify--image{
    height: 16px; 
    width: 20px;
    background-color:#25272E;
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
    margin-top: 80px;
    width: 1545px;
}
</style>