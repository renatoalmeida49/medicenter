<template>
    <footer>
        <div class="container flexColumn">
            <div class="footer_menu">
                <div class="fm_1">
                    <a href="">
                        ...
                    </a>
                </div>
                <div class="fm_2">
                    <a href="">
                        ...
                    </a>
                </div>
                <div class="fm_3">
                    <a href="">
                        ...
                    </a>
                </div>
            </div>
        

            <div class="footer_area">
                <div class="footer_areaitem">
                    <div class="widget_title">
                        <div class="widget_title_text">Medicenter Clinic</div>
                        <div class="widget_title_bar"></div>
                    </div>
                    <div class="widget_body">
                        ...
                    </div>
                </div>
                <div class="footer_areaitem">
                    <div class="widget_title">
                        <div class="widget_title_text">Latest News</div>
                        <div class="widget_title_bar"></div>
                    </div>
                    <div class="widget_body">
                        ...
                    </div>
                </div>
                <div class="footer_areaitem">
                    <div class="widget_title">
                        <div class="widget_title_text">Latest Tweets</div>
                        <div class="widget_title_bar"></div>
                    </div>
                    <div class="widget_body">
                        ...
                    </div>
                </div>
            </div>

            <div class="footer_copy">
                @Copyright - Todos os direitos reservados
            </div>
        </div>
    </footer>
</template>

<script>
export default {

}
</script>

<style scoped>
/* FOOTER */

footer {
	display: flex;
	justify-content: center;
	background-color: #1e1e1e;
}

.footer_menu {
	display: flex;
	flex-wrap: wrap;
}

.fm_1, .fm_2, .fm_3 {
	flex: 1;
	color: white;
	min-width: 208px;
}

.fm_1 {
	background-color: #39aae1;
}

.fm_2 {
	background-color: #0079c7;
}

.fm_3 {
	background-color: #2b4c99;
}

.footer_area {
	display: flex;
	flex-wrap: wrap;
}

.flexColumn {
	flex-direction: column;
}

.footer_areaitem {
	flex: 1;
	color: white;
	min-width: 208px;
}

footer .widget_title_text {
	color: white;
}

.footer_copy {
	border-top: 1px solid #2c2c2c;
	height: 40px;
	line-height: 40px;
	color: #5c5c5c;
	font-size: 0.75rem;
	margin-top: 30px;
}

.footer_menu a {
	display: block;
	text-decoration: none;
	padding: 20px;
	color: white;
}
</style>