
<template>
    <ul>
        <li>
            <NuxtLink to="/">Home</NuxtLink>
        </li>
        <li>
            <NuxtLink to="/about">About</NuxtLink>
        </li>
        <li>
            <NuxtLink to="/contact">Contact</NuxtLink>
        </li>
        <li>
            <NuxtLink to="/raju">Raju</NuxtLink>
        </li>
        <li>
            <NuxtLink to="/manoj">Manoj</NuxtLink>
        </li>
    </ul>
</template>

<style scoped>
a{
    text-decoration: none;
}
ul {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    gap: 2rem;
}

ul li {
    background-color: blueviolet;
    color: #fff;
    padding: 5px;
    border-radius: 5px;
}
.router-link-active{
    background-color: #888;
    color: #fff;
}
</style>