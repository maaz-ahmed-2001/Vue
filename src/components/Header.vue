<template>
    <header>
        <nav>
            <div id="logo">
            <h3>Spacespot</h3>
            </div>
            <div>
                
                <input type="search" name="search" placeholder="Start your search"/>
            </div>
            <div id="id">
                <h3>Maaz</h3>
                <img src="data:image/jpeg;base64,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"/>
            </div>   
        </nav>
    </header>
</template>
<script>
export default{
    name : "Header",
    
}


</script>
<style scoped>
*{
    margin: 0;
    padding: 0;

}
header{
    width: 100%;
    height: 12vh;
    box-shadow: 0px 0px 5px 1px rgb(177, 177, 177);
}
nav{
    height: 12vh;
    width: 100%;
    display: flex;
    justify-content: space-around;
    align-items: center;
    
}
div{
    height: fit-content;
    width: fit-content;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 10vh;
}
input{
    outline: none;
    border: none;
    box-shadow: 0px 3px 10px 0px rgb(209, 209, 209);
    border-radius: 20px;
    height: 5vh;
    width: 325px ;
    margin: 20px;
    padding-left: 15px;
}
img{
    border-radius: 50%;
    height: 40px;
    width: 40px;
}
#id{
    display: flex;
    justify-content: space-around;
    align-items: center;
    width: fit-content;
}
#id h3{
    margin-right: 25px;
}
#logo{

}
h3{
    font-weight: 300;
    color:#444;
}

</style>