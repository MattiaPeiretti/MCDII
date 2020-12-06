<template>
<div class="container-databar">
    <div class="content">
        <clock class="clock"></clock>
        <div class="quick-actions">
            <a><span>Share</span> <svg width="18" height="20" viewBox="0 0 18 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M15 14.08C14.24 14.08 13.56 14.38 13.04 14.85L5.91 10.7C5.96 10.47 6 10.24 6 10C6 9.76 5.96 9.53 5.91 9.3L12.96 5.19C13.5 5.69 14.21 6 15 6C16.66 6 18 4.66 18 3C18 1.34 16.66 0 15 0C13.34 0 12 1.34 12 3C12 3.24 12.04 3.47 12.09 3.7L5.04 7.81C4.5 7.31 3.79 7 3 7C1.34 7 0 8.34 0 10C0 11.66 1.34 13 3 13C3.79 13 4.5 12.69 5.04 12.19L12.16 16.35C12.11 16.56 12.08 16.78 12.08 17C12.08 18.61 13.39 19.92 15 19.92C16.61 19.92 17.92 18.61 17.92 17C17.92 15.39 16.61 14.08 15 14.08Z" />
                </svg>
            </a>
            <a><span>Donate</span> <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M12 2C6.48 2 2 6.48 2 12C2 17.52 6.48 22 12 22C17.52 22 22 17.52 22 12C22 6.48 17.52 2 12 2ZM13.41 18.09V20H10.74V18.07C9.03 17.71 7.58 16.61 7.47 14.67H9.43C9.53 15.72 10.25 16.54 12.08 16.54C14.04 16.54 14.48 15.56 14.48 14.95C14.48 14.12 14.04 13.34 11.81 12.81C9.33 12.21 7.63 11.19 7.63 9.14C7.63 7.42 9.02 6.3 10.74 5.93V4H13.41V5.95C15.27 6.4 16.2 7.81 16.26 9.34H14.3C14.25 8.23 13.66 7.47 12.08 7.47C10.58 7.47 9.68 8.15 9.68 9.11C9.68 9.95 10.33 10.5 12.35 11.02C14.37 11.54 16.53 12.41 16.53 14.93C16.52 16.76 15.15 17.76 13.41 18.09Z" fill="black" />
                </svg>
            </a>
        </div>
        
        <div class="credits">
            <span>A website by <a href="https://mattiapeiretti.com/" target="_blank">Mattia Peiretti</a> Opensouce <a href="https://github.com/MattiaPeiretti/MCDII" target="_blank">Repo</a></span>
        </div>

    </div>
</div>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
.container-databar {
    height: 22px;
    background-color: var(--databarBackgroundColor);
    position: fixed;
    bottom: 0;
    right: 0;
    left: 0;

    .content {
        width: 100%;
        display: flex;
        align-items: center;
        color: var(--textDarkBackgroundColor);
        font-size: 14px;
        line-height: 22px;

        span {
            height: 22px;
        }

        a {
            color: var(--textDarkBackgroundColor);
            padding: 0 4px;
            height: 22px;
            background-color: var(--databarBackgroundColor);
            border-bottom: 2px solid var(--databarBackgroundColor);
            border-top: 1px solid var(--databarBackgroundColor);
            transition: .1s;
            

            &:hover {
                background-color: var(--databarForegroundColor);
                border-bottom: 2px solid var(--databarForegroundColor);
                border-top: 1px solid var(--databarForegroundColor);
                color: var(--databarBackgroundColor);
                cursor: pointer;

                path {
                    fill: #ff4d00;
                }

            }

            svg {
                height: 15px;
                vertical-align: middle;
                padding-bottom: 2px;
                margin-left: 0;
                padding-left: 0;

                path {
                    fill: white;
                }
            }

            span {
                margin-right: -3px;
            }

        }

        .clock {
            margin-left: 10px;
        }

        .credits {
            margin-right: 10px;
        }

        .quick-actions {
             margin-left: auto;
        }

        .quick-actions, .credits {
             padding: 0 5px;
        }
    }
}
</style>
