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
        <article class="table-container">
            <!-- Блок с таблицей -->
            <p class="table-header">ХОД</p>
            <p class="timer-header">
                <!-- {{ timerCount }} -->
                {{ displayMinutes }}:{{ displaySeconds }}
            </p>

            <p class="parametres">Параметры и требования</p>
            <p class="user-1">Участник №1</p>
            <p class="user-2">Участник №2</p>
            <p class="user-3">Участник №3</p>
            <p class="user-4">Участник №4</p>
        </article>
    </div>
</template>

<script>
export default {
    name: "TradeTable",
    data() {
        return {
            timerCount: 120,
            displaySeconds: "0" + 0,
            displayMinutes: "0" + 2,
        };
    },

    computed: {
        _seconds: () => 1,
        _minutes() {
            return this._seconds * 60;
        },
        _hours() {
            return this._minutes * 60;
        },
        _days() {
            return this._hours * 24;
        },
    },
    watch: {
        timerCount: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount--;
                        const seconds = Math.floor(
                            (this.timerCount % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount % this._hours) / this._minutes
                        );

                        this.displayMinutes =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
    },
};
</script>

<style scoped lang="scss">
$text-color: brown;
$table-text-color: darken(lightblue, 30%);

.container {
    margin: 10px 20px;
}

.table-container {
    display: grid;
    grid-template-columns: 2 1 1 1 1;
    grid-template-rows: 2 2 auto auto auto auto auto auto;
}

.header-trade {
    font-size: 26px;
    color: $text-color;
    margin-bottom: 0.5rem;
}

.table-header {
    grid-column: 1/2;
    grid-row: 1/2;
    color: $table-text-color;
    // display: flex;
    margin-top: 2rem;
    width: 15rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.timer-header {
    grid-column: 2/3;
    grid-row: 1/2;
    color: $text-color;
    width: 15rem;
    margin-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.parametres {
    grid-column: 1/2;
    grid-row: 2/3;
    color: $table-text-color;
    text-transform: uppercase;
    margin-top: 3rem;
    width: 15rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

@mixin users {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 15rem;
    color: $table-text-color;
}

.user-1 {
    grid-column: 2/3;
    grid-row: 2/3;
    @include users;
}

.user-2 {
    grid-column: 3/4;
    grid-row: 2/3;
    @include users;
}

.user-3 {
    grid-column: 4/5;
    grid-row: 2/3;
    @include users;
}

.user-4 {
    grid-column: 5/6;
    grid-row: 2/3;
    @include users;
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
