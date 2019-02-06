<template>
    <Page class="page">
        <ActionBar class="action-bar">
            <Label class="action-bar-title" text="Home"></Label>
        </ActionBar>

        <GridLayout>
            <Label class="info" horizontalAlignment="center" verticalAlignment="top">
                <FormattedString>
                    <Span class="fa" text.decode="&#xf135; "/>
                    <Span :text="message"/>
                </FormattedString>
            </Label>
            <Label class="web-message" horizontalAlignment="center" verticalAlignment="center" v-bind:text="strFromWeb">

            </Label>

            <Button horizontalAlignment="center" verticalAlignment="bottom" style="margin-bottom: 20;" @tap="getDataFromWeb">Ściągnij dane z sieci...</Button>
        </GridLayout>
    </Page>
</template>

<script>
    import axios from "axios";

    export default {
        data() {
            return {
                strFromWeb: "Blank"
            };
        },

        computed: {
            message() {
                return "Blank {N}-Vue app";
            }
        },

        methods: {
            async getDataFromWeb() {
                console.log("Loading data from WEB...");
                try {
                    let response = await axios.get("https://live.mpk.czest.pl/api/locations/621dd03b-95f8-40c8-add1-1d4bdc4bdc5b");
                    this.strFromWeb = response.data.name;

                } catch(err) {
                    this.strFromWeb = "Wystąpił błąd!!!";
                    console.log(err);
                }
            }
        }
    };
</script>

<style scoped lang="scss">
    // Start custom common variables
    @import '../app-variables';
    // End custom common variables

    // Custom styles
    .fa {
        color: $accent-dark;
    }

    .info {
        font-size: 20;
    }

    .web-message {
        font-weight: bold;
        font-size: 30;
    }
</style>
