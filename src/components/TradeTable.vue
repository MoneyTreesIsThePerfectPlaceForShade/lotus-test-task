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
            <!-- Таймер -->
            <p v-show="active120" class="timer-header timer-1">
                {{ displayMinutes1 }}:{{ displaySeconds1 }}
            </p>
            <p v-show="active240" class="timer-header timer-2">
                {{ displayMinutes2 }}:{{ displaySeconds2 }}
            </p>
            <p v-show="active360" class="timer-header timer-3">
                {{ displayMinutes3 }}:{{ displaySeconds3 }}
            </p>
            <p v-show="active480" class="timer-header timer-4">
                {{ displayMinutes4 }}:{{ displaySeconds4 }}
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
            timerCount1: 120,
            timerCount2: 240,
            timerCount3: 360,
            timerCount4: 480,
            displaySeconds1: "0" + 0,
            displayMinutes1: "0" + 2,
            displaySeconds2: "0" + 0,
            displayMinutes2: "0" + 2,
            displaySeconds3: "0" + 0,
            displayMinutes3: "0" + 2,
            displaySeconds4: "0" + 0,
            displayMinutes4: "0" + 2,
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
        active120() {
            if (this.timerCount1 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active240() {
            if (this.timerCount2 >= 120 || this.timerCount2 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active360() {
            if (this.timerCount3 >= 120 || this.timerCount3 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
        active480() {
            if (this.timerCount4 >= 120 || this.timerCount4 <= 0) {
                return false;
            } else if (this.timerCount1 > 0) {
                return true;
            } else return true;
        },
    },
    watch: {
        timerCount1: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount1--;
                        const seconds = Math.floor(
                            (this.timerCount1 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount1 % this._hours) / this._minutes
                        );

                        this.displayMinutes1 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds1 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount2: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount2--;
                        const seconds = Math.floor(
                            (this.timerCount2 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount2 % this._hours) / this._minutes
                        );

                        this.displayMinutes2 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds2 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount3: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount3--;
                        const seconds = Math.floor(
                            (this.timerCount3 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount3 % this._hours) / this._minutes
                        );

                        this.displayMinutes3 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds3 =
                            seconds < 10 ? "0" + seconds : seconds;
                    }, 1000);
                }
            },
            immediate: true,
        },
        timerCount4: {
            handler(value) {
                if (value > 0) {
                    setTimeout(() => {
                        this.timerCount4--;
                        const seconds = Math.floor(
                            (this.timerCount4 % this._minutes) / this._seconds
                        );

                        const minutes = Math.floor(
                            (this.timerCount4 % this._hours) / this._minutes
                        );

                        this.displayMinutes4 =
                            minutes < 10 ? "0" + minutes : minutes;
                        this.displaySeconds4 =
                            seconds < 10 ? "0" + seconds : seconds;
                        if (
                            this.timerCount1 <= 0 &&
                            this.timerCount2 <= 0 &&
                            this.timerCount3 <= 0 &&
                            this.timerCount4 <= 0
                        ) {
                            this.timerCount1 = 120;
                            this.timerCount2 = 240;
                            this.timerCount3 = 360;
                            this.timerCount4 = 480;
                        }
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
    color: $text-color;
    width: 15rem;
    margin-top: 2rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.timer-1 {
    grid-column: 2/3;
    grid-row: 1/2;
}

.timer-2 {
    grid-column: 3/4;
    grid-row: 1/2;
}

.timer-3 {
    grid-column: 4/5;
    grid-row: 1/2;
}

.timer-4 {
    grid-column: 5/6;
    grid-row: 1/2;
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
