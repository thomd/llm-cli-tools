#!/usr/bin/env -S uv run -q -s
# vim:ft=python
# /// script
# requires-python = ">=3.8"
# dependencies = [
#     "rich",
# ]
# ///

import sys
import signal
from rich.console import Console
from rich.live import Live
from rich.markdown import Markdown
from rich import print as rprint

MARKDOWN_STYLE = {
    "code_theme": "ansi_dark",
    "justify": "left",
}

class MarkdownRenderer:
    def __init__(self):
        self.console = Console(highlight=True)
        self.md_content = "\n"
        self.live = None

    def create_markdown(self, content):
        return Markdown(content, **MARKDOWN_STYLE)

    @staticmethod
    def is_pipe_input():
        return not sys.stdin.isatty()

    def handle_signal(self, signum, frame):
        if self.live:
            self.live.stop()
        sys.exit(0)

    def render_stream(self):
        try:
            with Live(self.create_markdown(""), console=self.console, refresh_per_second=10) as live:
                self.live = live
                while True:
                    chunk = sys.stdin.read(1)
                    if not chunk:
                        break
                    self.md_content += chunk
                    live.update(self.create_markdown(self.md_content))
        except UnicodeDecodeError as e:
            rprint(f"[red]Error: Invalid character encoding: {str(e)}[/red]")
        except Exception as e:
            rprint(f"[red]Error: {str(e)}[/red]")

    def run(self):
        signal.signal(signal.SIGINT, self.handle_signal)
        signal.signal(signal.SIGTERM, self.handle_signal)
        if not self.is_pipe_input():
            return
        self.render_stream()

def main():
    renderer = MarkdownRenderer()
    renderer.run()

if __name__ == "__main__":
    main()
