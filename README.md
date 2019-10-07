# Linotype

Linotype is a simple ruby implementation of the [Letterpress for iOS](http://www.atebits.com/letterpress/) game mechanic. Letterpress was created by [Loren Brichter](http://twitter.com/lorenb) and is [sold on iTunes](https://itunes.apple.com/us/app/letterpress-word-game/id526619424?ls=1&mt=8). Linotype是[Letterpress for iOS]（http://www.atebits.com/letterpress/）游戏机制的简单红宝石实现。 凸版印刷机是由[Loren Brichter]（http://twitter.com/lorenb）创建的，并且[在iTunes上出售]（https://itunes.apple.com/us/app/letterpress-word-game/id526619424?ls = 1＆mt = 8）。 Linotype用于编写其他程序，例如简单的玩家命令行游戏，作弊/模拟程序，基于Web的版本或您能想到的其他任何程序。 我的目标是社区将向该项目提交请求请求，以便程序可以共享一个公共引擎。

该项目的灵感来自于此 [tweet by Andy Baio](https://twitter.com/waxpancake/statuses/261966416507465728).

该项目始于 [@barelyknown](http://twitter.com/barelyknown).

## Installation

    $ gem install linotype

## Usage

该库使用内置的Ruby对象提供了一个非常简单的接口。 设计的目标是在内部使用面向对象的设计策略，但要保持公共接口非常简单以使其易于使用和扩展。

这是主要的公共方法的基本清单：

    >   game = Linotype::Game.new
    
    >   game.board
    =>  [[{:letter=>"N", :row=>0, :column=>0, :covered_by=>1, :defended=>true},
          {:letter=>"S", :row=>0, :column=>1, :covered_by=>1, :defended=>false},
          {:letter=>"L", :row=>0, :column=>2, :covered_by=>nil, :defended=>false},
          {:letter=>"K", :row=>0, :column=>3, :covered_by=>nil, :defended=>false},
          {:letter=>"W", :row=>0, :column=>4, :covered_by=>nil, :defended=>false}],
         [{:letter=>"T", :row=>1, :column=>0, :covered_by=>1, :defended=>true},
          {:letter=>"P", :row=>1, :column=>1, :covered_by=>1, :defended=>false},
          {:letter=>"Y", :row=>1, :column=>2, :covered_by=>nil, :defended=>false},
          {:letter=>"E", :row=>1, :column=>3, :covered_by=>1, :defended=>false},
          {:letter=>"E", :row=>1, :column=>4, :covered_by=>nil, :defended=>false}],
         [{:letter=>"L", :row=>2, :column=>0, :covered_by=>1, :defended=>false},
          {:letter=>"O", :row=>2, :column=>1, :covered_by=>nil, :defended=>false},
          {:letter=>"L", :row=>2, :column=>2, :covered_by=>nil, :defended=>false},
          {:letter=>"Z", :row=>2, :column=>3, :covered_by=>nil, :defended=>false},
          {:letter=>"Z", :row=>2, :column=>4, :covered_by=>nil, :defended=>false}],
         [{:letter=>"T", :row=>3, :column=>0, :covered_by=>nil, :defended=>false},
          {:letter=>"B", :row=>3, :column=>1, :covered_by=>nil, :defended=>false},
          {:letter=>"W", :row=>3, :column=>2, :covered_by=>nil, :defended=>false},
          {:letter=>"M", :row=>3, :column=>3, :covered_by=>nil, :defended=>false},
          {:letter=>"F", :row=>3, :column=>4, :covered_by=>nil, :defended=>false}],
         [{:letter=>"B", :row=>4, :column=>0, :covered_by=>nil, :defended=>false},
          {:letter=>"O", :row=>4, :column=>1, :covered_by=>nil, :defended=>false},
          {:letter=>"F", :row=>4, :column=>2, :covered_by=>nil, :defended=>false},
          {:letter=>"M", :row=>4, :column=>3, :covered_by=>nil, :defended=>false},
          {:letter=>"V", :row=>4, :column=>4, :covered_by=>nil, :defended=>false}]] 
    
    >   # Takes about 8 seconds on a laptop -- brute force solution
    >   game.potential_plays
    =>  ["WORD","MATCHES","FROM","DICTIONARY","IN","AN","ARRAY"]
    
    >   next_play = game.best_next_play
    
    >   game.play(*next_play[:coordinates])
    =>  true
    
    >   game.moves.last.to_hash
    =>  { :player=>1,
          :word=>"SPLENT",
          :valid=>true,
          :coordinates=>[[0, 1], [1, 1], [2, 0], [1, 3], [0, 0], [1, 0]],
          :invalid_reason=>nil,
          :player_sequence=>1,
          :total_sequence=>1,
          :score => {
            :defended_before=>0,
            :covered_before=>0,
            :defended_after=>2,
            :covered_after=>6,
            :defended=>2,
            :covered=>6}
          }

    >   game.scores
    =>  {1=>2, 2=>0}

    #   pass by playing a nil move
    >   game.play
    =>  true
    
    >   game.play
    =>  true
    
    >   game.over?
    =>  true
    
    >   game.winner
    =>  1
    
## Dictionary
The default dictionary is based on the the [Internet Scrabble Club's TWL06 dictionary](http://www.isc.ro/en/commands/lists.html). Any dictionary can be used by replacing the contents of the `words.txt` file in the `/lib/linotype/dictionary` directory.

## Feature Ideas

* Game board loading from iOS screen shot
* Word suggestions (faster)
* One player command line game
* Vowel/consonant ratio setting for random boards
* Built in dictionaries for different languages or topics

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
6. Thanks <3
