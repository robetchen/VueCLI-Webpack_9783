

<template>

 <v-main>

     <nav class="navbar navbar-expand-sm fixed-top" id="mainNav">
        <div class="container">
         
        </div>
          <div class="content">
            <div class="boxtable">
                <div class="div1">
                    <p class="title">Dashboard</p>
                    <table class="table" style="border-style: none;">
                        <thead>
                            <tr>
                                <th scope="col">No</th>
                                <th scope="col">Kecepatan Produk</th>
                                <th scope="col">Harga Kecepatan Produk</th>
                                <th scope="col"></th>
                            </tr>
                        </thead>
                        <tbody>
                       
                           
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </nav>
    
 </v-main>
</template>

<style scoped>


nav {
    display: flex;
    justify-content: space-around;
    align-items: center;
    min-height: 8vh;
    background-color: #f4f4f4;
    font-family: 'Montserrat', sans-serif;
    border-bottom: 8px solid #6c89d9;
}

nav .btn {
    color: black;
    cursor: pointer;
}

.logo {
    color: black;
    text-transform: uppercase;
    align-items: left;
    letter-spacing: 5px;
    font-size: 30px;
}

.toplogo {
    height: 100px;
    width: 100px;
}


/* BODY */

#app {
    display: flex;
    max-width: 100%;
    min-height: 100vh;
}

#app .sidebar {
    background-color: #6c89d9;
    min-width: 30vh;
}

#app .sidebar .body {
    margin-top: 60px;
    margin-bottom: auto;
}

#app .sidebar .body a {
    text-decoration: none;
}

#app .sidebar .body .item {
    color: #fafafa;
    border-bottom: 1px solid rgba(255, 255, 255, 0.2);
    padding: 18px 24px;
    font-size: 14px;
}

#app .sidebar .body .item:hover {
    background-color: #7e9ef7;
}

.active {
    background-color: #b4c7fb;
}

.content {
    width: 100%;
}

.content .boxtable .div1 .title {
    color: #6c89d9;
    font-size: 40px;
}

table {
    border-collapse: 0 solid black;
    width: 100%;
    font-size: 15px;
    text-align: center;
}

thead {
    background-color: #b4c7fb;
}

.boxtable {
    position: relative;
    display: flex;
    background-color: #f4f4f4;
    width: 100%;
    height: 100%;
    background-attachment: fixed;
}

.div1 {
    width: 97%;
    height: fit-content;
    margin-top: 100px;
    margin-left: 20px;
    display: inline-block;
    background-color: #f4f4f4;
}

</style>