# Tutorial Inery Task 3

## Get binary inery.cdt tools
```
wget -qO task3.sh https://raw.githubusercontent.com/sipalingnode/inery/main/task3.sh && chmod +x task3.sh && ./task3.sh
```

```
export PATH="$PATH:$HOME/inery.cdt/bin:$HOME/inery-node/inery/bin"
source $HOME/.bash_profile
```

```
mkdir -p $HOME/inrcrud
```

## Write Code
***kagak usah di edit langsung aja salin semuanya yang dibawah***
```
sudo tee $HOME/inrcrud/inrcrud.cpp >/dev/null <<EOF
#include <inery/inery.hpp>
#include <inery/print.hpp>
#include <string>

using namespace inery;

using std::string;

class [[inery::contract]] inrcrud : public inery::contract {
  public:
    using inery::contract::contract;


        [[inery::action]] void create( uint64_t id, name user, string data ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing == recordstable.end(), "record with that ID already exists" );
            check( data.size() <= 256, "data has more than 256 bytes" );

            recordstable.emplace( _self, [&]( auto& s ) {
               s.id         = id;
               s.owner      = user;
               s.data       = data;
            });

            print( "Hello, ", name{user} );
            print( "Created with data: ", data );
        }

         [[inery::action]] void read( uint64_t id ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing != recordstable.end(), "record with that ID does not exist" );
            const auto& st = *existing;
            print("Data: ", st.data);
        }

        [[inery::action]] void update( uint64_t id, string data ) {
            records recordstable( _self, id );
            auto st = recordstable.find( id );
            check( st != recordstable.end(), "record with that ID does not exist" );


            recordstable.modify( st, get_self(), [&]( auto& s ) {
               s.data = data;
            });

            print("Data: ", data);
        }

            [[inery::action]] void destroy( uint64_t id ) {
            records recordstable( _self, id );
            auto existing = recordstable.find( id );
            check( existing != recordstable.end(), "record with that ID does not exist" );
            const auto& st = *existing;

            recordstable.erase( st );

            print("Record Destroyed: ", id);

        }

  private:
    struct [[inery::table]] record {
       uint64_t        id;
       name     owner;
       string          data;
       uint64_t primary_key()const { return id; }
    };

    typedef inery::multi_index<"records"_n, record> records;
 };
EOF
```

## Compile Code
```
inery-cpp $HOME/inrcrud/inrcrud.cpp -o $HOME/inrcrud/inrcrud.wasm
```

## Unlock Wallet & Set Contract
***nama-akun diganti dengan nama akun yang di web inery***
```
cline wallet unlock -n nama-akun
```
***Masukkan password wallet kalian yang udah di simpen***

```
cline set contract nama-akun ./inrcrud
```

## Create, Read, Update, Destroy Contract
***nama-akun diganti dengan nama akun yang di web inery***
```
cline push action nama-akun create '[1, "asc", "salam dari asc"]' -p nama-akun --json
```

```
cline push action nama-akun read [1] -p nama-akun --json
```

```
cline push action nama-akun update '[ 1,  "salam dari asc"]' -p nama-akun --json
```

```
cline push action nama-akun destroy [1] -p nama-akun --json
```

***Done Langsung klik Finish di web inery***
