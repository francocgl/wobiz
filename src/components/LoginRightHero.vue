<template>
   <div class="col-lg-8 col-md-6 d-none d-md-block p-0 col">
       <div class="relative">
            <div class="text-button">
                <p>¿No tienes una cuenta en Wobiz?</p>
                <button class="btn btn-outline">Crea tu alerta</button>
            </div>
        <figure class="img-box vh-100">   
            <img src="@/assets/hero.png" alt="">
        </figure>
       </div>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.img-box img{
    object-position: right ;
}
.text-button{ 
    position: absolute;
    top: 42px;
    right: 10%;
    z-index: 1;
    align-items: center;
    display: none;
}
.text-button p{
    font-size: .8em;
    color: #fff;
    margin: 0 30px 0 0;
}
.text-button .btn.btn-outline{
    color: #e0e0e0;
    border-radius: .3rem;
    border:1px solid #e0e0e0;
    font-weight: 700;
    transition: all .6s ease-in-out;
    height: 35px;
    padding: 0 16px;
    font-size: .9em;
}

@media only screen
and (min-width : 961px) {
    .text-button{ display: flex;}

    @media(hover: hover) {
        .btn.btn-outline:hover{
            background-color: #e0e0e0;
            color: #000000;
        }
    }
}
</style>