<template>
    <div class="home">
        <Calculator></Calculator>
    </div>
</template>

<script>
// @ is an alias to /src
import Calculator from "@/components/Calculator";

export default {
    name: "Home",
    components: {
        Calculator: Calculator,
    },
};
</script>
