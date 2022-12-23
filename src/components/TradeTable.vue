<template>
    <div class="container">
        <header>
            <!-- Заголовок страницы -->
            <p class="header-trade">
                Ход торгов
                <strong
                    >Тестовые торги на ппарат ЛОТОС №2033564 (23.12.2022
                    08:00)</strong
                >
            </p>
            <hr />
            <p class="msg-for-traders">
                Уважаемые участники, во время вашего хода вы можете изменить
                параметры торгов, указанных в таблице:
            </p>
        </header>
        <article>
            <!-- Блок с таблицей -->
        </article>
    </div>
</template>

<script>
export default {
    name: "TradeTable",
};
</script>

<style scoped lang="scss">
$text-color: brown;
.container {
    margin: 10px 20px;
}

.header-trade {
    font-size: 26px;
    color: $text-color;
    margin-bottom: 0.5rem;
}

.msg-for-traders {
    display: inline-block;
    margin-top: 0.5rem;
    margin-left: 1rem;
    color: $text-color;
    background-color: lighten($text-color, 50%);
    border-radius: 0.5rem;
    padding: 0.3vw;
}

hr {
    background-color: rgb(178, 178, 178);
}
</style>
